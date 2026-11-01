# Money Flows Playbook

Apply this on top of the core principles in SKILL.md when designing or reviewing any screen where money is shown or moved: balances, send and pay flows, currency conversion, transaction lists, transaction details, receipts and payout or funding status.

A good money screen answers three questions before the user acts: **How much exactly? Where is it going? What happens next?** After the user acts, it answers one more: **Where is my money right now?** Uncertainty costs more here than anywhere else. Users who are unsure don't just hesitate, they contact support, retry and send twice.

## Before you start

Identify:
- **Which currencies appear**, and whether any have no minor unit (JPY, UGX, XOF, XAF) or three decimals (KWD, BHD, OMR). Design every amount slot for these, not just for two-decimal currencies.
- **Who pays the fees**, sender or recipient, and whether a fee is fixed, a percentage or built into the exchange rate.
- **Every state a transaction can be in**, as the backend defines it. The UI must have a designed answer for each one, including the rare ones.

## Showing amounts

- **Format with the platform, never by hand.** Use `Intl.NumberFormat` (or the platform equivalent) with the currency code, so separators, decimals and symbol placement follow the currency and locale. No hard-coded `$`, no `toFixed(2)` for every currency. The platform's default decimals come from CLDR and occasionally differ from ISO 4217 or from what your provider settles in, so when they disagree, set `minimumFractionDigits` and `maximumFractionDigits` from your currency config.
- **Keep money out of floating point.** Amounts arrive and are calculated as integer minor units or decimal strings, and are converted for display only at the edge. A display bug that shows `₦0.30000000000000004` destroys trust instantly.
- **Disambiguate symbols in cross-border contexts.** `$` means many currencies. When more than one currency is on screen, or the user is sending abroad, show the ISO code ("1,250.00 USD", `currencyDisplay: "code"`) or a prefixed symbol ("US$"). Use `currencyDisplay: "narrowSymbol"` only where a single currency is certain.
- **Use tabular figures** (`font-variant-numeric: tabular-nums`) for any amount that updates live or sits in a column, so digits don't jitter. Check the font actually supports them. Right-align amount columns.
- **Never use colour alone for direction.** A debit gets a real minus sign (`−`, not a hyphen) or a "Sent" label as well as its colour. Credits can take a `+` and a restrained green. Most rows in a list stay neutral; full-strength red is for failures, not ordinary spending.
- **Size by importance.** The amount being sent or the balance is the largest element on its screen. Supporting amounts (fees, rate, limits) are visibly secondary but never hidden or greyed below AA contrast.
- **Balances.** Say which balance it is when more than one exists ("Available", "Pending"). Offer a hide/show toggle with an accessible label ("Show balance"). Show when it was last updated if it can be stale.

## Amount input

- Large, centered or left-aligned with the currency beside it, never a small generic text field.
- Numeric keyboard on mobile (`inputmode="decimal"`, or `inputmode="numeric"` for zero-decimal currencies), separators inserted as the user types without jumping the cursor, pasted values like "₦1,200.50" cleaned rather than rejected.
- Respect the currency's decimals: no decimal point for zero-decimal currencies, and up to three digits where the currency uses three.
- Context directly under the field: available balance, and limits only when they matter ("Max ₦5,000,000 per transfer"). A one-tap "Max" or preset amounts help repeat users.
- Validate at the right moment. "Exceeds your balance of ₦12,400.00" appears as the user types past it, in the field's own space, and says the number they need.

## Exchange rates and fees

- **Show both sides at all times.** "You send" and "They receive", each with its currency, linked so editing one updates the other.
- **Rate in plain form**: "1 USD = 1,530.20 NGN". Avoid inverted or unlabelled rates.
- **Itemise before confirming**: amount, fee, rate, total debited, amount received. If the fee is in the rate, say so. Fees that appear for the first time on the last screen read as hidden fees.
- **Rate validity.** If a quote expires, show the time remaining, and when it refreshes, tell the user what changed before they confirm. Never silently confirm at a different rate.

## The send flow

1. **Amount** (and currencies).
2. **Recipient.** When the system can resolve the account holder's name from the account number, show the resolved name prominently before the user continues. It is the user's best protection against a typo sending money to a stranger. Saved and recent recipients come first.
3. **Review.** One screen that shows everything that will happen: recipient name and account (partially masked), amount sent, fees, rate, amount received, total debited and expected arrival time. Each part is editable with one tap back to that step.
4. **Authorise** (PIN, biometrics). Keep the amount and recipient visible on the authorisation step so the user never confirms blind.
5. **Status.** See below.

Rules across the flow:
- **The primary action states the consequence**: "Send ₦50,000.00", not "Submit", "Continue" or "Confirm". Update it live.
- **Prevent double submission.** Disable the action immediately on tap and show progress inside the button. A second tap during a slow network is the most common cause of duplicate payments. Pair this with an idempotency key on the request, so a retried request can't create a second payment.
- **Never offer a blind retry.** If the request times out, the outcome is unknown: check the transaction's status before showing "Try again", and show the "Checking status" state below until you know.
- **Progress is visible** on multi-step flows (step count or a short stepper), and back navigation never loses entered values.

## Transaction status

Every status needs three things: **a plain-language label, what it means for the money, and what happens next (with a time if known).** Say only what is true: tell the user where the money actually is, not a generic reassurance.

| State | Label | Message pattern |
|---|---|---|
| Unknown (request timed out) | Checking status | "We're confirming this with the bank. Please don't send it again; we'll update you shortly." |
| Processing | Processing | "Usually arrives within 2 minutes. We'll notify you." |
| Action required | Action needed | What the user must do and why: "Enter the code we sent to finish this transfer." |
| Under review | Under review | "We're running a routine check. ₦50,000.00 is on hold in your wallet. Most reviews finish within 24 hours." |
| Delayed | Taking longer than usual | Where the money is now ("₦50,000.00 has left your wallet and is with the recipient's bank") and when you expect it to clear. |
| Completed | Sent / Received | Amount, recipient, time, reference. |
| Failed | Failed | What failed in plain words, and **where the money is now**: "₦50,000.00 has been returned to your wallet." |
| Cancelled | Cancelled | Who cancelled it and confirmation that nothing was debited, or when it will be returned. |
| Reversed / refunded | Refunded | When it was returned and to where. |

- **Pending is not an alarm.** Use a neutral or informational colour for in-progress states. Reserve red for failed, and pair it with the reassurance about the money.
- **Status chips use one shape and short words.** Chips across the list must be readable in a glance and consistent with the detail screen.
- **Announce changes.** When a status updates on screen, announce it to screen readers (e.g. an `aria-live="polite"` region).
- **Show a timeline** on the detail screen for multi-leg transactions (initiated → processing → sent → received), with timestamps on completed steps.
- **Give a next action** on every non-final or failed state: try again, change details, contact support with the reference pre-filled.

## Transaction lists and details

- Each row: who or what (name or merchant), when (relative for recent, date for older), amount with direction, and status only when it isn't "completed". Most rows should be calm.
- Group by date with subtle headers. Search and filter by amount, recipient and status for anything beyond a few screens.
- **References and IDs**: monospace or tabular figures, truncated in the middle if long, with a copy button and a "Copied" confirmation.
- **Dates and times** include the time zone on details and receipts.
- **Receipts** are shareable (image or PDF) and include amount, fees, rate, sender, recipient, date and time with time zone, reference and status. They look like a document, not a screenshot of the app.

## Trust and tone

- Errors explain and never blame: "We couldn't reach the recipient's bank. Nothing was debited." beats "Transaction error".
- Celebrate success briefly and calmly. A check and a clear summary beat confetti when someone has just moved rent money.
- Security and verification messages are specific about why and what to do, not vague warnings.
- Hide sensitive values (full account numbers, balances on shared screens) by default where it makes sense, with an obvious reveal.

## Money flow checks

Add these to the general audit:

1. Amounts formatted by currency and locale, not by hand; correct decimals for every supported currency.
2. Currency is unambiguous wherever more than one could apply.
3. Amount columns use tabular figures and right alignment.
4. Debits and credits are distinguishable without colour.
5. Fees, rate and total debited are visible before confirmation, not added on the last step.
6. Recipient's resolved name is shown before the user commits.
7. Primary action states the amount; it disables on tap, and a timeout leads to a status check, not a blind retry.
8. Every transaction state has a label, a money-location message and a next step.
9. Pending states don't use alarm colours; failed states say where the money is.
10. References are copyable; receipts include time zone and reference.

## Stress cases

- A very large amount (₦1,000,000,000.00) and a very small one (0.01).
- A zero-decimal currency (UGX) and a three-decimal one (KWD) in the same list.
- A long recipient or business name, and a name that couldn't be resolved.
- A rate that expires while the user is on the review screen.
- A slow network, a repeated tap on the send button, and a request that times out with no response.
- A transfer held for review, and one that needs the user to act.
- A transfer that fails, and one that fails and is later reversed.
- A user with no transactions yet.
