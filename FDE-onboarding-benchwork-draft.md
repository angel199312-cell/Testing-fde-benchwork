# FDE Benchwork — Employee Onboarding

Status: Draft — saved for later. Do not run yet.

## Prompt Framework

**Goal:** Set up an onboarding list for new employees.

**Users:** New employees and HR coordinator.

**Task:** Prepare an onboarding checklist that follows this sequence:

1. Send the offer letter with the employer's signature already attached, an employee e-signature option, and a clickable Date field that automatically records the current date and time when the employee signs.
2. After the employee's receipt of the offer letter is confirmed, send the employment contract with an e-signature option for both parties.
3. After the employment contract is sent, send the onboarding email with the first-day date, arrival time, and reporting address.

**Constraints:** Follow the sequence strictly. Block contract sending until offer-letter receipt is confirmed. Block onboarding-email sending until the contract has been sent. Require the first-day date, arrival time, and reporting address before sending the onboarding email. Do not mark a step complete without confirmation that it occurred.

**Working interpretation:** "Offer letter received" means confirmed receipt by the employee. The offer letter has the employer's signature attached before sending and offers an employee e-signature option. The employment contract offers e-signature options for both parties. Completion of signatures is not a prerequisite for the next step under this draft. This interpretation can be revised if signed acceptance is intended.

**Output:** Checklist with checkboxes.

## Onboarding Checklist

Employee name: [To be provided]
HR coordinator: [To be provided]

### 1. Offer Letter

- [ ] Offer letter includes an employee e-signature option.
- [ ] Employer's signature is attached to the offer letter before sending.
- [ ] Offer letter includes a clickable Date field that automatically records the current date and time, including the time zone, when the employee signs. The recorded value remains fixed after signing.
- [ ] Offer letter sent to the employee.
- [ ] Employee receipt of the offer letter confirmed.

### 2. Employment Contract

Start only after all offer-letter checklist items are complete.

- [ ] Employment contract includes an employee e-signature option.
- [ ] Employment contract includes an employer e-signature option.
- [ ] Employment contract sent to the employee.

### 3. Onboarding Email

Start only after all employment-contract checklist items are complete.

- [ ] First-day date included: [Date].
- [ ] Arrival time included: [Time and time zone].
- [ ] Reporting address included: [Full address].
- [ ] Onboarding email sent to the employee.

## Acceptance — Two Test Cases

### Test Case 1: Complete the steps in order

**Given:** Employee and employer details, both documents, and the first-day date, arrival time, and reporting address are available.

**When:** HR sends the offer letter, the employee signs it using the e-signature option, HR confirms employee receipt, sends the employment contract, and then sends the onboarding email.

**Expected:** The offer letter has the employer's signature attached before sending and provides an employee e-signature option. Its clickable Date field automatically records the date and time of the employee's signature, including the time zone, and retains that value when reopened later. The employment contract offers e-signatures for both parties. The email contains all three arrival details. The recorded event order is offer sent → offer receipt confirmed → contract sent → onboarding email sent. Checkboxes are marked complete only for confirmed actions.

### Test Case 2: Prevent out-of-order actions

**Given:** The offer letter has been sent, but employee receipt is not confirmed; the employment contract has not been sent.

**When:** HR attempts to send the contract and onboarding email.

**Expected:** Both actions are blocked and their sent checkboxes remain unchecked. After receipt is confirmed, contract sending becomes available. Onboarding-email sending remains blocked until the contract is sent and the date, time, and reporting address are provided.

