# Prototype: Send Message from Chart [DO-14563]

## Runbook

- [Read Me](https://client.timagineer.com/auth//ica/DO-14563/README.md)
- [Prototype](https://client.timagineer.com/auth/ica/DO-14563/)

## Testing the Prototype

### Typeahead Search
Type 3+ characters in To or Cc fields. Try: `sar`, `mar`, `jen`, `dav`, `amy`

### Error Toast
Run in browser console:
```js
showToast('error', 'Failed to send message')
```

## Design Notes

- **Popover, not modal** — lightweight, stays anchored to trigger
- **Client chip is locked** — auto-mapped from chart context, can't be removed
- **Cc always visible** — no toggle to reveal it
- **Send validation** — needs at least one To recipient AND either subject or body content
- **Discard** — closes immediately, no confirmation
- **Motion** — popover scales/fades in; toasts slide up from bottom-right
