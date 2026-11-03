# AP Invoice Pipeline

Accounts-payable invoice automation — an 18-flow RPA suite that carries invoices from Outlook into Yardi, validates payable status and notifies stakeholders.

## What it does

End-to-end AP invoice processing on a desktop automation agent: invoice intake from Outlook, database staging, Yardi invoice entry, payable/EFT status checks and stakeholder notifications — 18 flows, 180 steps.

## Flow (high level)

```
Outlook intake → stage in database
      ↓
RPA flows (18) — each step: pass → next step, fail → recovery flow
      ↓
Payable + EFT verification
      ↓
Notify stakeholders
```

## Logic

- Branching execution: every step declares a pass → next flow and fail → fallback flow, with per-step timeouts
- Recovery flows handle popups, odd screen states and missing invoices, branching back into the main chain instead of stopping
- The suite self-heals rather than halting; a dedicated agent device runs it unattended

## Problems solved

- **RPA breaks on unexpected UI states** → self-healing recovery flows instead of hard stops
- **Scattered invoice mail** → monitored mailbox intake with a database working table as the single source of truth
- **Payment status uncertainty** → automated payable + EFT verification before notifying stakeholders

*Implementation scripts are intentionally not published — this repository documents the approach and results.*

---

*High-level overview only — this project is a confidential client engagement; implementation details are not published.*
