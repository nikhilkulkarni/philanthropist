# Requirements: Donor–Debtor Matching App

*Working title: swipe-based platform matching high-net-worth donors with people seeking debt relief. Draft v0.1 for review.*

## 1. Purpose and Scope

A mobile-first app and website with a Tinder-like swipe experience. **Donors** (billionaires and other high-net-worth individuals) browse **debtor** profiles and swipe right to commit to paying off all or part of a debt. Funds are collected into a platform-controlled escrow account, the debtor's debt is verified with their lender, and the payoff is then executed.

**Stage 1** delivers the full user journey and operating workflow *without* direct bank or card integration. Money movement and verification are handled through assisted or manual processes run by platform operations. **Stage 2** replaces those manual steps with live integrations.

**Terminology note:** the UI should use dignified, neutral language (for example "Applicant" or "Seeker" instead of "needy debtor"). "Donor" and "Debtor" are used in this document for clarity only.

## 2. User Roles

| Role | Description |
| --- | --- |
| Debtor | Lists one or more debts, tells their story, and creates a profile. |
| Donor | Creates a profile and preferences, links a funding source with limits, and swipes on debtor profiles. |
| Platform Admin / Ops | Verifies identities, moderates profiles, reconciles escrow, and manages payoffs. |
| Compliance / Support | Handles disputes, flagged cases, and audit requests. |

## 3. Assumptions and Constraints

- A1. Stage 1 has no live API integration with banks, card networks, or lenders.
- A2. The platform operates a real escrow or client-money account, held with a regulated partner (to be confirmed with legal).
- A3. Initial launch targets a single country and currency; multi-currency is a later phase.
- A4. Every payoff is made directly to the lender, never to the debtor.
- A5. Both parties must pass identity verification before any pledge is binding.

## 4. Stage 1: Detailed Functional Requirements

### 4.1 Accounts and Onboarding

- FR-1.1: Sign up with email or phone plus password or one-time passcode, with optional social login.
- FR-1.2: At sign-up the user chooses a role (Donor or Debtor). One account holds one role.
- FR-1.3: Mandatory email and phone verification.
- FR-1.4: Identity verification (KYC) in Stage 1: user uploads a government ID and a selfie; Ops reviews and approves or rejects in the admin console, with a reason on rejection.
- FR-1.5: Donors have an additional wealth or source-of-funds declaration, reviewed by Ops.
- FR-1.6: Acceptance of Terms, Privacy Policy, and role-specific consent (for example, consent to share debt details with the lender).
- FR-1.7: Account states: Pending, Verified, Suspended, Closed.

### 4.2 Debtor Profile

- FR-2.1: Basic fields: display name (or first name only), age range, photo(s), city, region and country, occupation, household situation (for example, dependents), and languages.
- FR-2.2: Profile story: short headline (140 characters), "Why I need help" (up to 1,500 characters), and "What this would change for me" (up to 500 characters).
- FR-2.3: Optional fields: hobbies and interests, community involvement, a short intro video, and a pledge on how they will pay it forward.
- FR-2.4: Photos and the full legal name can be hidden until a match is confirmed (privacy mode, on by default).
- FR-2.5: Debtors choose which demographic attributes are visible on the profile. Any attribute used for donor filtering (see 4.4) is voluntary.
- FR-2.6: Profile completeness indicator, and a profile cannot go live until it is verified and at least one debt listing is approved.

### 4.3 Debt Listing (Debtor)

- FR-3.1: A debtor can add multiple debts. Each debt includes:
  - Debt type: student loan, credit card, home mortgage, personal loan, medical or health expense, auto loan, other.
  - Lender or institution name.
  - Account or reference number (masked after entry).
  - Original amount, current outstanding amount, interest rate, and monthly payment.
  - Delinquency status (current, late, in collections, in default).
  - Amount requested: full or partial, and the specific amount.
  - Optional: amount the debtor can co-pay, and a co-pay schedule.
  - Reason this debt arose and why the debtor deserves relief (free text, per debt).
- FR-3.2: Supporting documents: latest statement or letter from the lender, and optionally hardship evidence such as medical bills. Allowed formats are PDF, JPG, and PNG, with a size limit.
- FR-3.3: Each debt listing moves through the states Draft → Submitted → Under Review → Approved (Live) / Rejected / Needs Info → Matched → Validated → Funded → Paid Off → Closed.
- FR-3.4: Each debt is independently swipeable. A donor can fund a single debt, not necessarily the whole profile.
- FR-3.5: Edits to amounts or lender after approval send the listing back to review.
- FR-3.6: Maximum number of live debts per debtor and maximum amount per debt are configurable by Admin.

### 4.4 Donor Profile and Preferences

- FR-4.1: Basic profile: display name (with an anonymous option), photo or avatar, city and country, bio, philanthropic interests, and causes they care about.
- FR-4.2: Visibility options: fully public, first name only, or anonymous until payoff completes.
- FR-4.3: Preferences (used to filter and rank the swipe deck):
  - Debt types (multi-select).
  - Location or region of the debtor.
  - Other debtor attributes (see the compliance note below).
  - Amount range per debt (minimum and maximum).
  - Payoff mode: full only, partial allowed, or either.
  - Maximum percentage or amount the donor will cover per debt.
  - Co-pay requirement: none, required (minimum percentage), or preferred.
  - Debt status: current, delinquent, or in collections.
  - Maximum number of pledges per month or per year.
  - Total budget per month or per year.
- FR-4.5: Preferences are editable at any time, apply to future decks, and never cancel existing pledges.
- **Compliance note:** filtering by protected characteristics (for example race, religion, or ethnicity) carries legal and platform-policy risk. This is an open item (see Section 8). The wireframe will include a configurable "Other attributes" preference block that legal can enable, restrict, or remove without redesign.

### 4.5 Donor Funding Source and Limits

- FR-5.1: A donor adds a funding source, either a bank account or a credit card, with a nickname.
- FR-5.2: Stage 1: details are captured as a *declared* funding source (masked details and a verification document), verified manually by Ops. No live debit is made.
- FR-5.3: Donor-set limits: per-pledge cap, daily, monthly, and annual caps, and an overall lifetime cap.
- FR-5.4: A swipe that would breach any limit is blocked with a clear message and a prompt to raise the limit.
- FR-5.5: Donors can pause all pledging with one toggle.
- FR-5.6: A secondary confirmation (biometric or passcode) is required for any pledge above a threshold the donor configures.

### 4.6 Discovery and Swiping (Donor)

- FR-6.1: Card-based swipe deck showing the debtor's photo (or avatar if in privacy mode), headline, debt type, amount requested, amount remaining, and a short "why" excerpt.
- FR-6.2: Tap a card to open the full profile and debt detail, including documents' verification badges (not the documents themselves).
- FR-6.3: Swipe left to pass (the profile is hidden from that donor). Swipe right to start a pledge.
- FR-6.4: Swipe up to Save for Later (a shortlist).
- FR-6.5: Right swipe opens a **confirmation sheet** before anything binding happens: amount, full or partial, co-pay terms, platform fee (if any), funding source, and a clear statement of what the donor is committing to. The donor taps **Confirm Pledge** to proceed.
- FR-6.6: Undo for the last pass. There is no undo after a confirmed pledge, except within a short cooling-off window (configurable, default 24 hours, before funds are marked received).
- FR-6.7: Deck ranking: preference match first, then urgency, then recency. No pay-to-boost.
- FR-6.8: A debt that is fully pledged by another donor disappears from decks immediately. If several donors fund the same debt partially, the platform tracks the funded percentage.
- FR-6.9: Optional report button on every profile.

### 4.7 Match and Pledge

- FR-7.1: A confirmed right swipe creates a **Pledge** (Donor, Debt, amount, terms) in the state *Pledged – Awaiting Funds*.
- FR-7.2: The debt is reserved for that donor for a configurable window (default 72 hours) while funds are collected. If the window lapses, the pledge expires and the debt returns to the deck.
- FR-7.3: The debtor receives a "You've been matched" notification showing the donor's chosen visibility level (anonymous or named), the amount, and next steps.
- FR-7.4: The debtor can accept or decline a match. Declines require a reason and release the debt. (Optional per product decision.)
- FR-7.5: A Match screen is shown to both parties with a status tracker.

### 4.8 Escrow Funding (Stage 1: Assisted)

- FR-8.1: After a pledge, the donor sees payment instructions for the platform escrow account, including a unique reference code per pledge.
- FR-8.2: Donor uploads proof of transfer, or Ops marks funds received after reconciling the escrow bank statement.
- FR-8.3: Pledge states: Pledged → Funds Claimed → Funds Received in Escrow → Released to Lender → Completed. Failure states: Expired, Cancelled, Refunded.
- FR-8.4: An internal escrow ledger records every movement (in, hold, release, refund), tied to a pledge and a debt. The ledger is immutable and exportable.
- FR-8.5: Under- and over-payments are flagged for Ops, who resolve by refund or top-up.
- FR-8.6: Refund rules: if debt validation fails, the lender rejects payment, or the debtor declines, funds are refunded to the donor's original source, minus any disclosed non-refundable fee.
- FR-8.7: Platform fee (if any) is shown on the confirmation sheet and in the ledger.

### 4.9 Debt Validation (Debtor)

- FR-9.1: When funds reach escrow, the debtor is prompted to validate the debt with their financial institution.
- FR-9.2: Stage 1 validation methods: (a) upload an official, dated payoff or balance letter or statement from the lender; (b) authorise the platform to contact the lender; (c) Ops phone or email verification with the lender.
- FR-9.3: Validation checks include that the account holder name matches the verified identity, the balance matches the listing within tolerance, and the account is open.
- FR-9.4: Outcomes: Validated, Validated with Adjustment (amount corrected, and the donor is notified and re-confirms if the amount rises), or Failed.
- FR-9.5: Validation deadline (default 7 days). If missed, the pledge is cancelled and funds are refunded.
- FR-9.6: Co-pay: if the debtor agreed to a co-pay, proof of their contribution (receipt or an escrow payment) is required before release.

### 4.10 Payoff Execution (Stage 1: Manual)

- FR-10.1: After validation, Ops initiates the payment from escrow directly to the lender's account, using the lender-provided payoff instructions.
- FR-10.2: Ops records the payment reference and uploads the transfer confirmation.
- FR-10.3: Ops (or the debtor) obtains lender confirmation that the payoff posted. The debt is then marked Paid Off.
- FR-10.4: Both parties receive a completion notice, with a receipt for the donor and a payoff confirmation for the debtor.
- FR-10.5: Optional thank-you note from debtor to donor (moderated), and optional impact update.

### 4.11 Notifications and Messaging

- FR-11.1: Push, email, and SMS notifications for each state change and each action required.
- FR-11.2: Stage 1 in-app messaging is limited to platform-mediated, moderated messages (thank-you notes), with no free-form direct chat and no exchange of contact details before payoff is complete. This protects both sides.
- FR-11.3: A user-level notification preferences screen.

### 4.12 Admin and Operations Console

- FR-12.1: Queues for KYC review, profile moderation, debt-listing review, escrow reconciliation, validation review, payoff execution, refunds, and reports.
- FR-12.2: Case view with full timeline, documents, notes, and an audit trail of every Ops action.
- FR-12.3: Role-based access: maker-checker (two-person approval) is required for any release or refund of funds.
- FR-12.4: Configuration: fee percentage, limits, reservation windows, validation deadlines, allowed debt types, and preference attributes.
- FR-12.5: Dashboards: funds in escrow, pledges by state, time-to-payoff, rejection reasons, and fraud flags.
- FR-12.6: Export of ledger and audit data for finance and regulators.

### 4.13 Trust, Safety and Fraud Controls

- FR-13.1: Duplicate-debt detection, so the same debt cannot be listed by two accounts or funded twice.
- FR-13.2: Document tampering checks (manual review in Stage 1).
- FR-13.3: Blocking and reporting, plus a moderation queue for stories, photos, and thank-you notes.
- FR-13.4: Scam protection for donors: no direct transfers to debtors, and warning banners on any off-platform contact attempt.
- FR-13.5: Sanctions, PEP, and AML screening of both parties (manual or via a screening service) during onboarding.
- FR-13.6: Dispute process for both parties, with an SLA.

### 4.14 Settings, Support and Legal

- FR-14.1: Help center, FAQs, and a support ticket form.
- FR-14.2: Data export and account deletion (with legal retention exceptions).
- FR-14.3: Receipts and donation records for donor tax purposes, where applicable.
- FR-14.4: Clear in-app disclosures: the platform is not a lender or a charity (unless structured as one), how escrow works, and the tax treatment guidance.

## 5. Non-Functional Requirements

- NFR-1 **Security:** encryption in transit and at rest; field-level encryption for account numbers and ID documents; MFA for donors and admins; secrets management; regular penetration testing.
- NFR-2 **Privacy:** data minimisation; role-based visibility of financial data; compliance with applicable data-protection law (GDPR, CCPA, or local equivalent).
- NFR-3 **Auditability:** immutable logs for all pledge, ledger, and admin actions.
- NFR-4 **Availability:** 99.5% or better for Stage 1.
- NFR-5 **Performance:** swipe deck loads in under 2 seconds on a typical mobile connection; card transitions at 60 fps.
- NFR-6 **Platforms:** iOS, Android, and responsive web (the admin console is web only).
- NFR-7 **Accessibility:** WCAG 2.1 AA, with swipe alternatives (buttons) for every swipe gesture.
- NFR-8 **Localisation-ready:** externalised strings, with currency and date formatting.
- NFR-9 **Scalability:** architecture should allow Stage 2 integrations without redesign (see Section 7).

## 6. Screen Inventory for the Wireframe (Stage 1)

**Shared:** Splash, Role selection, Sign-up and login, Verification (ID and selfie), Notifications centre, Settings, Help.

**Debtor:** Profile builder, Add or edit debt, Debt documents upload, My debts dashboard, Match detail and status tracker, Debt validation flow, Payoff confirmation and thank-you.

**Donor:** Profile and visibility settings, Preferences, Funding source and limits, Swipe deck, Full profile and debt detail, Pledge confirmation sheet, Shortlist, Pledge tracker, Escrow payment instructions and proof upload, Impact and receipts.

**Admin web console:** Dashboard, KYC queue, Listing review, Escrow reconciliation, Validation review, Payoff execution, Disputes, Configuration, Audit log.

## 7. Stage 2: High-Level Requirements

- S2-1 **Payment collection:** direct integration with card networks and bank rails (for example ACH, UPI, SEPA, or card acquiring via a regulated payment partner) for tokenised funding sources, with automatic debit on confirmed pledge, enforcement of donor limits in real time, and automated refunds.
- S2-2 **Escrow automation:** programmatic escrow or client-money accounts, with automatic ledger reconciliation against bank feeds.
- S2-3 **Lender integration:** APIs or secure channels to major lenders and loan servicers for instant debt verification (balance, status, account holder) and for direct payoff posting with confirmation.
- S2-4 **Account verification:** open-banking or account-aggregation style linking for debtors to validate debts, and instant donor bank verification.
- S2-5 **Automated KYC/AML:** third-party identity, sanctions, and fraud screening integrated into onboarding and transaction monitoring.
- S2-6 **Automation of operations:** auto-approval for low-risk cases; Ops handles exceptions only.
- S2-7 **Advanced matching:** better recommendation ranking, pooled funding (multiple donors per debt), recurring or conditional pledges, and impact reporting.
- S2-8 **Communication:** optional, moderated direct messaging after payoff and consent from both parties.
- S2-9 **Tax and reporting:** automated receipts, annual statements, and regulatory reporting.
- S2-10 **Scale and expansion:** multi-currency and multi-country, public API for partners, and analytics for donors and the platform.

## 8. Risks and Open Questions (Need Decisions Before Build)

1. **Regulatory structure:** holding and moving other people's money may require money-transmitter, payment-institution, or similar licences, or a licensed partner. Escrow structure and fund-flow legal review are needed first.
2. **Charity versus gift:** is this a charitable donation (tax-deductible, requiring a registered entity) or a private gift? This changes tax receipts, gift-tax implications for donors, and potentially taxable debt-forgiveness income for debtors.
3. **Filtering by race and other protected attributes:** this may breach anti-discrimination law and app-store policies, and could be reputationally damaging. Recommend legal review, and consider limiting preferences to non-protected criteria (debt type, region, hardship type, profession, and so on).
4. **Fraud:** fake hardship stories, fabricated debts, and collusion between accounts. Strong verification and manual review are the main controls in Stage 1.
5. **Debtor dignity and privacy:** profiles reveal sensitive financial and personal data, so privacy mode, consent, and moderation are central to the design.
6. **Platform fee model:** none, a percentage added on top, or deducted from the donation.
7. **Partial and shared funding:** can multiple donors fund one debt in Stage 1, or only one donor per debt?
8. **Launch geography and currency:** which country and which debt types are in scope first (mortgages and medical debt behave very differently from credit cards).
9. **Reservation and cooling-off windows:** the defaults proposed above need business sign-off.
10. **Debtor acceptance step:** can a debtor decline a donor (for example, over conditions or visibility)?

## 9. Next Step

Once you have reviewed and amended this draft, we will move to the wireframe. Proposed order: (1) donor swipe flow, (2) debtor profile and debt listing, (3) match, escrow, and validation tracker, (4) admin console.
