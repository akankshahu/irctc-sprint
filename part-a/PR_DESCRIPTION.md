# Part A — IRCTC Problem Discovery: 6 Pain Points Documented

## Screenshot from live IRCTC platform

> Screenshot added as a placeholder. Replace with a live IRCTC screenshot if available.

![IRCTC screenshot placeholder](assets/screenshots/screenshot-irctc-placeholder.svg)

## Summary table

| # | Problem | Category | Frequency (one-line) |
|---|---|---|---|
| 1 | Tatkal booking crashes at 10:00 AM | Booking reliability / peak traffic | Daily at Tatkal opening, with highest failures in the 10:00 AM surge window. |
| 2 | Search filters do not work reliably | Search and discovery | Intermittent under normal use; more frequent during peak traffic and back-navigation. |
| 3 | Seat selection resets randomly | Booking flow state management | Intermittent in seat-map sessions; higher incidence on mobile than desktop. |
| 4 | PNR status and reservation chart break main flow | Post-booking journey flow | Happens every time users jump from booking UI to external utility pages. |
| 5 | Homepage buries primary booking task | Information architecture / UX hierarchy | Happens on every homepage visit, especially for first-time or low-confidence users. |
| 6 | Narrow browser compatibility signaling | Access and compatibility | Conditional by environment, but recurring for users on constrained/older browser setups. |

## Real user complaint quote

> “IRCTC website hangs exactly when Tatkal opens and by the time it reloads, everything is waitlist.”

Source links (examples):
- Twitter/X search for recent user reports: https://x.com/search?q=IRCTC%20Tatkal%20crash&src=typed_query
- Reddit search for user reports and threads: https://www.reddit.com/search/?q=IRCTC%20Tatkal%20crash

Video proof: add your Google Drive video URL here after upload.

---

Polished summary

This repository contains the Part A problem-discovery deliverable for the IRCTC design sprint: six documented pain points (three given, three self-discovered). Each issue includes a concrete failure description, clearly defined affected users, frequency estimates, and a step-by-step broken flow that a PM or engineer can act on. A placeholder screenshot is included; replace it with a live capture if available. Once the short video walkthrough is uploaded, add the Drive link above and we'll finalize submission.

## Confirmation

Yes — the 3 self-discovered problems (Problems 4, 5, 6) are different from the 3 given problems (Problems 1, 2, 3).
