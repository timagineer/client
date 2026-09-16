# Availability Blocks: Design Spec

## Problem

Clinicians define recurring availability windows (e.g., "Intakes 9–12", "Telehealth 1–4"). These blocks often overlap. Front desk staff need to see what time is bookable and for what appointment types—without visual clutter obscuring appointments.

## Core Insight

Availability blocks are **background context**, not foreground content. They answer "what *can* be scheduled here?" while appointments answer "what *is* scheduled here?"

---

## Rendering Concepts Explored

| Concept | Approach | Pros | Cons |
|---------|----------|------|------|
| **A** | Stack full-width, z-order by start time | Simple | Deep overlaps obscure earlier blocks |
| **B** | Alpha transparency + blend | Shows all layers | Colors muddy with 3+ overlaps |
| **B2** ✓ | Union fill + labels + tooltip | Clean, scannable | Requires tooltip for full detail |
| **B3** | Hatched/striped overlaps | Visual distinction | Busy; accessibility concerns |
| **C** | Side-by-side columns | All blocks visible | Wastes horizontal space |

---

## Recommended: Concept B2

**Principle:** Render the *union* of overlapping blocks as a single visual region. Communicate *what* overlaps via labels and tooltips rather than stacked colors.

### Rendering Rules

1. **Single background fill** — Use the color of the topmost (latest-starting) block
2. **Corner label** — Show block name top-right; for overlaps, show the topmost block's name
3. **"+N more" badge** — Bottom-right badge when multiple blocks overlap (only visible when no appointment covers that region)
4. **Tooltip on hover** — Lists all overlapping blocks with type, time, and clinician

### Why B2

- **Scannable** — One muted background per region; eyes go to appointments
- **Discoverable** — Badge signals "there's more here"; tooltip provides full detail
- **Accessible** — No reliance on transparency blending or pattern recognition
- **Performant** — No compositing; simple DOM

---

## Visual Encoding

### Availability Blocks
- **Background:** OKLCH lightness -95 step (very light tint)
- **Border:** OKLCH -70 step (subtle)
- **Label text:** Neutral `--text-1` (not colored)

### Appointments
- **Left border (4px):** Appointment *type* (intake, established, telehealth, crisis, group)
- **Right border (4px):** Appointment *status* (arrived, confirmed, cancelled, no-show)
- **Body:** White card with shadow

### Color Palette (OKLCH)
| Type | Hue | Use |
|------|-----|-----|
| Cerulean | 217° | Intakes |
| Violet | 295° | Established |
| Jade | 161° | Telehealth |
| Orange | 56° | Crisis |
| Fuchsia | 336° | Group |

---

## Tooltip Behavior

| Hover Target | Tooltip Shows |
|--------------|---------------|
| Appointment | Patient, time, type, status + **"Within:"** section listing underlying blocks |
| Block (no appt) | Block name, type, time, clinician. If overlaps: **"+N more"** badge → hover for list |

This keeps appointment-focused workflows fast while making availability discoverable.

---

## Implementation Notes

- Blocks render in a layer behind appointments (`z-index` lower)
- `pointer-events: none` on block backgrounds; labels/badges are interactive
- Overlap detection: compare `start < other.end && end > other.start`
- Keyboard shortcut: `a` toggles availability visibility globally

---

## Open Questions

1. Should collapsed/hidden availability still influence booking validation?
2. Multi-provider day view: show unified availability or per-provider columns?
3. Month view: show availability at all, or just appointment density?
