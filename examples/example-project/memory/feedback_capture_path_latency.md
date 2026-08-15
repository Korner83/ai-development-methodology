---
name: capture-path-latency
description: Before adding anything to the `tinker capture` code path — the 300ms budget is measured cold, including process start.
metadata:
  type: feedback
  pinned: true
---

The `tinker capture` path has a **p95 budget of 300ms measured cold** — process start to note
durably written. That is the KPI in [P1 — Capture](../pillars/P1_capture.md), and it is the
product claim: capture has to feel free, or people stop capturing.

This has been blown twice by changes that looked unrelated to performance:

- A config-file read added at startup so capture could honour a `default_tags` setting (2026-05-14).
- Lazy-loading the calendar integration on the capture path "so it's there when we need it"
  (2026-05-20). It was needed on ~2% of captures and cost every one of them.

Both were reasonable-looking changes. Neither author was thinking about the budget, because
nothing in the code says the budget exists.

**Why:** the budget is a *cold-start* number, so it has no headroom to absorb work — there is no
warm process to amortize against, and every millisecond added to startup is added to every single
capture. A change that would be invisible in a long-running service is directly user-visible here.
Measuring after the fact catches it late, when the design already assumes the work happens inline.

**How to apply:** if a change adds work to the capture path — a file read, a network call, an
import with side effects, a lazily-initialized module — the default answer is **no**. Move it off
the path: do it on first *use* of the feature that needs it, or in `tinker recent`, or in a
background write after the note is durable. If it genuinely must be inline, measure cold p95
before and after and put both numbers in the item body.

**Pinned** because it is load-bearing and its own success makes it look inert: nobody has blown the
budget since it was written down, which is exactly what a working rule looks like. Low reference
frequency is not grounds to archive it.
