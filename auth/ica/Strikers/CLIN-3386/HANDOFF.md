# CLIN-3386 Telehealth Waiting Room — Design Handoff Notes

**Prototype:** `index-003.html`
**Last updated:** October 17, 2026

---

## Behavior Decisions

### Group accordion default state
Expand if any member has status `waiting` or `insession`. Collapse if all members are `scheduled`.

### Group accordion click target
Both the chevron button and the group name text toggle the accordion.

### Ad hoc sessions
Ad hoc (unscheduled) sessions display an "Ad hoc" badge inline in the Name cell. Individual sessions only for MVP — group ad hoc is Phase 2 (CLIN-4372).

### Guardian / Not billed participants
Guardians and non-billed external participants show a "Guardian" badge in the Name cell. Their Copay checkbox is disabled. Hovering the disabled checkbox shows a tooltip: "Not billed".

### Copay disabled states
Disabled copay checkboxes show contextual tooltips on hover:
- Absent patient → "Marked absent"
- Guardian / non-billed participant → "Not billed"
- Not yet arrived → "Not yet arrived"
- Session ended, already collected → "Already collected"

### Session status labels (action buttons)
Use action verbs, not status labels:
- Patient in waiting room, not yet admitted → **Admit**
- Session active (staff or provider) → **Join**
- Session ended → **Restart**
- Scheduled, not yet arrived → **Admit** (disabled)
- Absent → **Admit** (disabled)
- Group with arrivals → **Admit all**

---

## Open Questions / Deferred

| Topic | Decision | Notes |
|-------|----------|-------|
| Group default expand | Smart (by activity) | See above |
| Date range picker | Deferred from MVP | Day view only for now |
| Date toolbar alignment | Stub — spacing between date and nav group needs refinement at production | |
| Group ad hoc creation | Phase 2 | Individual only in MVP (CLIN-4372) |
| Create note dropdown | Agreed, undesigned | CLIN-4377 |
| Soft delete / confirm | Agreed | Story TBD |
| Staff chat panel | Out of scope (use BBB native) | |
| Session recording | Out of scope | |

---

## References

- Jira: [CLIN-3386](https://icanotes.atlassian.net/browse/CLIN-3386)
- Child epics: CLIN-4352 (Core), CLIN-4356 (Group/Ad hoc), CLIN-4357 (Tracking/Reporting)
- README: `README.md`
- Meeting notes: Oct 7, 2026
