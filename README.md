# Philanthropist

A swipe-based app that matches high-net-worth donors with people seeking debt relief. Donors browse verified debtor profiles and swipe right to pledge to pay off all or part of a debt. Funds are held in escrow, the debt is verified with the lender, and the payoff is paid directly to the lender.

> **Status:** design phase. This repository describes the requirements, wireframes, app screens and an animated walkthrough. There is no working backend yet.

## What is in this project

| Item | Description | Link |
|---|---|---|
| Requirements | Detailed Stage 1 and high-level Stage 2 requirements | [./docs/specs/](https://github.com/nikhilkulkarni/philanthropist/blob/main/docs/specs/Requirements%20Donor%E2%80%93Debtor%20Matching%20App.md) |
| App screens | 18 purple-themed screens on a canvas (donor, debtor, shared, admin) | [./docs/specs/](https://github.com/nikhilkulkarni/philanthropist/blob/main/docs/ui/Philanthropist%20App%20Screens.html) |
| Animated walkthrough | About 70 seconds, self-playing, with Pause and Replay | .. |
| `philanthropist-walkthrough.html` | Source file of the walkthrough, a single self-contained HTML page | this folder |

## How it works

1. **Debtor** creates a profile and lists one or more debts, each with a reason for needing relief.
2. **Donor** creates a profile, preferences and a funding source with spending limits.
3. Donor swipes through debtor cards: right to pledge, left to pass, up to save for later.
4. A confirmed pledge moves the donor's money into the platform's escrow account.
5. Debtor validates the debt with their lender.
6. Funds are released from escrow directly to the lender. The debtor never receives the money.

## Roles

- **Debtor:** lists debts and tells their story.
- **Donor:** sets preferences and limits, then pledges.
- **Admin / Ops:** reviews identities and listings, reconciles escrow, and executes payoffs.

## Screens

**Donor:** Discover (swipe deck), debtor detail, Confirm pledge, Preferences and limits, Profile and visibility, Shortlist, My pledges, Fund escrow.

**Debtor:** Profile builder, Add a debt, My debts, Validate debt, Loan paid off and thank-you.

**Shared:** Welcome and role choice, Verify identity, Match tracker, Notifications.

**Admin (web):** Escrow reconciliation.

## Stage 1 and Stage 2

**Stage 1 (no live bank or card integration)**
- Identity checks, listing review and debt validation are done by Ops using uploaded documents.
- Donors pay into escrow by transfer using a unique reference code, and Ops marks funds received.
- Ops pays the lender from escrow, and approvals for releases and refunds need two people.

**Stage 2 (high level)**
- Automatic debit from the donor's card or bank, with limits enforced in real time.
- Automated escrow reconciliation and direct lender integration for verification and payoff.
- Automated KYC, AML and sanctions screening.
- Pooled funding by several donors, recurring pledges, tax receipts and multi-country support.

## Open decisions

These need answers before any build starts:

- **Licensing:** holding and moving other people's money may require money-transmitter or similar licences, or a licensed partner.
- **Gift or charity:** this affects tax receipts, donor gift tax and whether debt forgiveness is taxable income for debtors.
- **Filtering by protected traits:** filtering debtors by race or similar traits carries legal and app-store risk. The design keeps this as an Admin-controlled option, off by default.
- **Fraud controls:** fake stories and fabricated debts are the main risk, so Stage 1 relies on manual review.
- **Fee model:** no fee, a fee added on top, or a fee deducted from the gift. Currently shown as `[TBD]`.
- **Shared funding:** whether several donors can fund one debt in Stage 1.

## Notes on the designs

- All names, amounts and lenders are **sample content**. Bracketed items such as `[TBD]` mark undecided details.
- Debtor photos are shown as initials, matching a privacy mode that reveals photos only after a match.
- Swipe actions have button alternatives for accessibility.

## Running the walkthrough locally

Open `philanthropist-walkthrough.html` in any modern browser. It needs no build step or network access. Use the Pause and Replay buttons below the phone. To make a video, screen-record the page.

## Not yet designed

Settings and help, disputes and reporting, empty and error states, the decline-a-match step, and the remaining admin queues (KYC, listing review, validation, payoffs, configuration).
