# Design Brief: Practice SMS Settings & Client Appointment Policy


## Problem

Practices need one place to control client text messaging across appointment reminders, telehealth, and shared documents and forms. Today, SMS controls live inside individual features, mostly Calendar. Practice-wide rules are also stored on each reminder template: the send window, whether clients can confirm or cancel, and the cancellation cutoff. As a result, one practice can end up with conflicting policies. For example, Reminder 1 can allow cancelling with no limit while Reminder 2 enforces 24 hours, so what a client can do depends on which text they reply to.

## Who it's for

The primary audience is practice owners and admins configuring the practice. A secondary audience is office managers, who maintain reminders day to day. Clients are affected by the outcome, because they see consistent rules across text, email, and the portal.

## Key insights

**Some of these are policies, not template properties.** Whether clients can confirm or cancel, and how late they can cancel, are practice decisions that apply to SMS, email, and the portal alike. They belong in one place, not repeated per template.

**Quiet hours are a channel rule.** The send window should apply to every SMS type, not just reminders. The exception is telehealth links, which are time-critical.

**Settings are already scattered.** The IA audit and meeting notes both point to a coming re-IA. This release should land where that re-IA is likely heading, so nothing has to move twice.

## Design principles

1. **Each setting has exactly one home.** Never put two switches on the same behavior.
2. **Policies live where the decision is made; channels live where messages are sent.** The client policy goes in Calendar, and SMS controls go in Communications.
3. **Every dependent screen shows the current state and links to where it's set.** Nobody should edit a template that will never send.
4. **Migration must never silently loosen a practice's rules.**

## Proposed solution

**Communications › SMS Settings (new tab).** This page has a master SMS switch, a global send window, and a toggle per message type: appointment reminders, telehealth, and documents and forms. Telehealth can skip the send window. The appointment reminders card shows the client policy read-only, with a link. The type list is a catch-all for future client-facing features.

**Calendar › Confirmations & Cancellations (new sub-tab).** This sets two practice-level rules that apply to SMS replies, email links, and the portal:
- **Confirmations:** whether clients can confirm (Yes/No), with no time cutoff.
- **Cancellations:** whether clients can cancel (Yes/No), and if Yes, how close to the appointment.

**Calendar › SMS/Text Appt Reminders (revised).** Each template keeps its lead time, message text, and a per-reminder on/off switch. Its confirm and cancel checkboxes now only control whether that text includes the prompt, and they're disabled when the policy says no. A new `{Reply Instructions}` tag renders only the reply options clients actually have, with a live preview. A status banner shows whether SMS is on and the current send window.

## Migration

- **Cancellation:** use the most restrictive value currently in place across templates, email, and the portal.
- **Confirmation:** turn it on if any channel allows it today. Confirming has no downside for the practice.
- **Send window:** use the narrowest existing window.
- Show admins a one-time notice explaining what moved and the value it was set to.
- Redirect old settings URLs and update the KB articles.

## Decisions needed from PM

1. Permissions: reuse `MessagingEnableSMSReminders` for the master switch, or create a new practice messaging permission.
2. Scope of telehealth SMS: practice-wide, per clinician, or both. Telehealth settings are user-level today.
3. Whether to include the late-cancellation message. It's proposed by design and not yet in scope.
4. Cancellation cutoff options: keep 1/3/24/48 hours, add 72, or allow free entry.
5. How the `SMSReminders` flag cutover works, given that legacy (id 9) and new (id 120) reminder pages exist today.

## Open questions for engineering and compliance

- Per-type configuration beyond what's designed. Candidates include STOP/opt-out handling, client-level SMS consent and how it overrides practice settings (TCPA), and sender number.
- Whether texts scheduled outside the send window are held until it opens or skipped.
- Whether any practice needs a confirmation cutoff.

## Risks

- For some practices, the effective cancellation policy gets stricter on one channel after migration. The one-time notice mitigates this.
- Existing reminder text may tell clients to reply to cancel after cancellations are turned off. The `{Reply Instructions}` tag and an inline warning mitigate this.
- Placing a new top-level Communications tab before the card sort validates it. This is a low risk: the proxy sort and the meeting both point the same way, and the tab starts narrow with SMS only.


## Out of scope

Moving email templates, Practice Forms, or staff Notifications into Communications. These wait for the card sort and the full re-IA.
