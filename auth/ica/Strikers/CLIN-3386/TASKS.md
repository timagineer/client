# CLIN-3386 Telehealth Waiting Room — Next Iteration Tasks

**Source:** Nov 3, 2026 design refinement meeting (Tim, Amit, Alex)

---

## 1. Date / Navigation Controls

- [ ] **1.1** Add `[ Today ][ < ][ > ]` quick-nav strip
  - Today always resets to single-day view ✅ locked
  - Chevrons move by the current span (±1 day in single-day, ±N days in range mode) ✅ locked
- [ ] **1.2** Add date range inputs (start date / end date)
  - Default state: today (single-day view)
  - Selecting a range switches to multi-day view
  - Chevrons shift the full span in multi-day mode
- [ ] **1.3** Merge Date and Time columns into a single **Date & Time** column

---

## 2. Header Filter Controls

- [ ] **2.1** Client autocomplete filter (combo box, matches name or chart ID)
- [ ] **2.2** Clinician autocomplete filter (combo box)
- [ ] **2.3** Status dropdown filter
- [ ] **2.4** Retain smart search bar (quick lookup by name)
- [ ] **2.5** Filters flex-wrap at narrow viewports

---

## 3. Action Buttons — Two Separate Buttons ✅ locked

**Decision:** Split into two buttons. Mixing session lifecycle and communication actions in one dropdown creates a god menu. Two buttons make categories legible at a glance.

### Session button (primary, contextual)

| State | Label | Enabled |
|---|---|---|
| Patient in waiting room | Admit | ✓ |
| Group with multiple waiting | Admit all | ✓ |
| Session active | Join | ✓ |
| Session ended | Restart | ✓ |
| Scheduled, no arrivals | Admit | ✗ disabled |
| Marked absent | Admit | ✗ disabled |

- [ ] **3.1** Implement contextual Session button with correct states
- [ ] **3.2** Disabled states show tooltip on hover (existing pattern)

### Send Link button (secondary, always enabled)

Dropdown: Email / SMS / Both / Copy link

- [ ] **3.3** Implement Send Link dropdown button
- [ ] **3.4** Always enabled — independent of Session button state
- [ ] **3.5** Copy link copies to clipboard + confirms with toast

---

## 4. Create Session

Button label: **Create session**

### 4.1 Existing client path
- [ ] Search by patient name or chart ID (autocomplete)
- [ ] Auto-populate email and/or phone on file
- [ ] If contact missing: inline input to add (saves to chart on submit)
- [ ] Send method: Email / SMS
- [ ] Time field: defaults to now, editable
- [ ] No DOB, no clinician (defaults to logged-in user)
- [ ] On create: new row appears at top of table (time-sorted ascending)

### 4.2 External client path
- [ ] First name + last name (required)
- [ ] Email (required)
- [ ] Time field: defaults to now, editable
- [ ] Send method: Email only (no SMS, no phone field)
- [ ] On create: same as above

---

## 5. Navigation / Placement

- [ ] **5.1** Telehealth Waiting Room as a Dashboard tab (provisional)
- [ ] **5.2** Note in prototype: temporary placement pending sidebar IA redesign

---

