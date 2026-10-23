# CLIN-3386: Telehealth Waiting Room

**Created:** 03/26  
**Status:** Open  
**Team:** Strikers

## Overview

Enable practices to create and manage Telehealth Waiting Rooms for individual and group sessions. This is a major parity gap — Plus currently cannot do group telehealth at all, and individual sessions drop patients straight into live rooms with no admit step.

## Epic Structure

### Parent Epic
- **CLIN-3386** — Telehealth Waiting Room (this epic)

### Child Epics

#### CLIN-4352: Telehealth Waiting Room Core
Foundation for individual sessions: persistent links, patient waiting page, dashboard, admit flow.

| Key | Story | Status |
|-----|-------|--------|
| CLIN-4355 | Foundation: feature flag, permissions, data model, service wiring | Open |
| CLIN-4358 | Integration-service telehealth adapter and per-person join URLs | Open |
| CLIN-4359 | Links at booking and appointment sync | Open |
| CLIN-4360 | Patient waiting page | Open |
| CLIN-4361 | Telehealth Waiting Room dashboard | Open |
| CLIN-4362 | Admit, Join, End, Restart | Open |
| CLIN-4363 | Resend, copy link, mark Absent | Open |
| CLIN-4364 | Reminders carry the persistent link | Open |

#### CLIN-4356: Group and Ad hoc Sessions
Multi-participant sessions, external invites, walk-ins, ad hoc creation.

| Key | Story | Status |
|-----|-------|--------|
| CLIN-4368 | Shared group session | Open |
| CLIN-4369 | External participants and walk-ins | Open |
| CLIN-4370 | Admit all arrived and multi-select resend | Open |
| CLIN-4371 | Group copay checkboxes | Open |
| CLIN-4372 | Ad hoc sessions | Open |
| CLIN-4373 | Roster invites | Open |

#### CLIN-4357: Live Session Tracking, Operations and Reporting
Real-time presence, auto-end, copay, notes, reports.

| Key | Story | Status |
|-----|-------|--------|
| CLIN-4374 | Video room events reach Plus: presence and Leave/End detection | Open |
| CLIN-4375 | Auto-end | Open |
| CLIN-4376 | Copay for individual sessions | Open |
| CLIN-4377 | Start a note from the dashboard | Open |
| CLIN-4378 | Camera/microphone guidance and audio-only fallback | Open |
| CLIN-4379 | Session Report | Open |
| CLIN-4380 | Session duration and presence reconciliation | Open |
| CLIN-4381 | Caseload Report and bell notification routing | Open |
| CLIN-4382 | Per-session audit view and observability | Open |

---

## Key Decisions (Oct 7 Meeting)

1. **"Join live session"** — action verb, not status label
2. **Session length column** — separate from wait time, starts when session begins
3. **Soft delete with confirmation** — for session removal
4. **Create note dropdown** — in waiting room table, generates linked note
5. **Date range picker deferred** — MVP uses day view with basic date controls
6. **Group ad hoc deferred to Phase 2** — individual ad hoc only in MVP
7. **Design sprints staggered** — at least one full sprint ahead of dev

---

## Session States

1. **Scheduled** — link exists, too early to join
2. **Waiting** — within 30-min window, not yet admitted
3. **Active** — in progress
4. **Ended** — finished, no new joins until restarted
5. **Restarted** — reactivated with same persistent link

---

## Dashboard Columns

| Column | Description |
|--------|-------------|
| Name | Patient/group name, appointment type badge, time |
| Arrived | Checkmark when patient enters waiting room |
| Admitted | Checkmark when staff admits |
| Copay | Checkmark when collected |
| Time in queue | Duration since arrival |
| Quick actions | Admit/In Session button, link, menu |

For groups: row shows rolled-up counts (e.g., "4/7 arrived"), expands to show individual participants.

---

## Key Workflows

### Individual Session
1. Appointment created → persistent link generated → sent at booking
2. Patient clicks link → DOB verification → waiting screen → "Arrived" status
3. Staff clicks Admit → patient enters session
4. Staff can Leave (stay active) or End (terminate for all)
5. Session can be Restarted with same link

### Group Session
1. Group appointment → one shared session, individual links per participant
2. Each participant arrives independently with own status
3. "Admit all arrived" or individual admits
4. Walk-ins can be added mid-session
5. Guardians/externals join by email only (no DOB)

### Ad Hoc (MVP: individual only)
1. Create session from dashboard without appointment
2. Search existing patient (DOB verification) or enter external (email only)
3. Same flow from there

---

## Permissions

Two new permissions:
- **View Telehealth Sessions** — see own sessions
- **View Telehealth Sessions for Other Clinicians** — see all (default for Staff/Admin)

Prerequisite: User must have Telehealth service personally activated.

---

## Out of Scope (MVP)

- Custom staff chat (use BBB native)
- Billing/claims handoff (deferred to billing team)
- Group copay automation (manual per participant)
- Group note-start shortcut
- Guardian/proxy distinction logic
- Static/reusable practice-level links
- Session recording
- Report exports, saved templates

---

## References

- [Product Brief](https://docs.google.com/document/d/1pH2YiZlDl-TBkCaYBckErlnidKQk1RSamOkzYX8UAZA/edit)
- [User Journeys](https://docs.google.com/document/d/1iHxINiwINOJD3TCVj19oq6p7nHLKTx-5YE6lN7auFiE/edit)
- PM Prototype: `telehealth-waiting-room-prototype(3).html`
