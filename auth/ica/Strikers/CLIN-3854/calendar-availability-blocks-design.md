# Availability Blocks: Design Spec

## Problem

Clinicians define recurring availability windows (e.g., "Intakes 9–12", "Telehealth 1–4"). These blocks often overlap. Front desk staff need to see what time is bookable and for what appointment types—without visual clutter obscuring appointments.

## Core Insight

Availability blocks are **background context**, not foreground content. They answer "what *can* be scheduled here?" while appointments answer "what *is* scheduled here?"

---

## Overlap Rendering: Topmost Wins

When availability blocks overlap, render with **shortest/most-specific block on top** (opaque). Hidden blocks discoverable via badge + tooltip.

### Rules
1. **Z-order by duration** — Shorter blocks on top
2. **Opaque fills** — No transparency blending
3. **Label** — "Clinician · Type · Time" top-right
4. **"+N more" badge** — Bottom-right when blocks hidden underneath
5. **Tooltip** — Lists all overlapping blocks on hover

### Why This Approach
- Clean, scannable backgrounds
- No muddy color blending with 3+ overlaps
- Badge signals hidden info; tooltip provides detail
- Works for accessibility (no pattern/transparency reliance)

---

## Appointment Cards

### Dual-Border Encoding
- **Left border:** Appointment *type* (intake, telehealth, crisis, etc.)
- **Right border:** Appointment *status* (confirmed, arrived, cancelled, etc.)

This gives at-a-glance scanning of both dimensions without icons or labels.

### Type Colors (left)
| Type | Hue Family |
|------|------------|
| Intake | Cerulean |
| Established | Violet |
| Telehealth | Jade |
| Crisis | Orange |
| Group | Fuchsia |

### Status Colors (right)
| Status | Hue Family |
|--------|------------|
| Scheduled | Violet |
| Confirmed | Blue |
| Arrived / Checked In | Teal |
| Occurred | Green |
| Cancelled | Amber |
| Late | Vermillion |
| No Show | Crimson |

---

## Tooltips

### Appointment Tooltip
- Patient name + time header
- Type and status shown as **mini-cards** with matching border treatment (type=left border, status=right border)
- "Within" section lists underlying availability blocks

### Block/Badge Tooltip
- Lists all blocks at that time: "Clinician · Type · Time"

---

## Calendar Grid

- **Quarter-hour ticks** in time gutter only (not full grid lines)
- **Hour lines** across columns
- **Sticky header** with subtle shadow on scroll
- **No vertical dividers** in header row
- **Toggle** to show/hide availability globally (keyboard: `a`)

---

## Prototype

See `availability-blocks-002.html` for interactive reference.

---

## Open Questions

1. Month view: Show availability or just appointment density?
2. Multi-provider views: Per-provider columns vs. unified?
