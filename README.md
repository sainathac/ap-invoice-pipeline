# AP Invoice Pipeline

Accounts-payable invoice automation — an 18-flow RPA suite that carries invoices from Outlook into Yardi, validates payable status and notifies stakeholders.

## Situation

AP invoices arrived scattered across Outlook and were processed into Yardi by hand. Earlier automation attempts kept dying on unexpected UI states — popups, odd screen shapes, missing invoices — and stakeholders had no reliable visibility into payable status.

## Task

I built the full desktop RPA suite that carries an invoice from mail intake all the way to Yardi entry, payable/EFT verification and stakeholder notification — designed to survive messy UI instead of stopping on it.

## Action

- I designed branching execution: every one of the 180 steps declares a pass -> next flow and a fail -> fallback flow, with per-step timeouts
- I built dedicated recovery flows for popups, odd screen states and missing invoices that branch back into the main chain rather than halting the run
- I staged incoming mail into a database working table so the suite always operates on a single source of truth
- I added automated payable + EFT verification before any stakeholder notification goes out, so status is checked, not assumed
- I run the suite unattended on a dedicated agent device

## Flow (high level)

```
Outlook intake -> stage in database
      |
RPA flows (18) -- each step: pass -> next step, fail -> recovery flow
      |
Payable + EFT verification
      |
Notify stakeholders
```

## Result

18 flows and 180 steps run end to end unattended; unexpected UI states trigger recovery instead of hard stops; payable status is verified automatically before anyone is notified; and the whole path from inbox to Yardi entry needs no manual touch.

*Implementation scripts are intentionally not published — this repository documents the approach and results.*

---

*High-level overview only — this project is a confidential client engagement; implementation details are not published.*
