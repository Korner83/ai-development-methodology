# Show HN draft

_Maintainer: edit to your voice before posting. Hacker News titles are the highest-leverage edit; spend most of the review time there._

---

## Title (pick one — A/B candidates)

**A.** Show HN: An AI development methodology built around the markdown + git you already use

**B.** Show HN: A 13-doc methodology for projects where humans and AI agents are peers

**C.** Show HN: AI Development Methodology — what to do when an AI just refactored your auth at 2am

**Title-writing notes:**

- HN titles work best when they describe what the thing IS, not what it promises. Title C has the most pull but risks sounding "promotional"; titles A and B are safer.
- Avoid superlatives ("best", "revolutionary"). HN sees through them within seconds.
- Avoid framing as a "framework" or "system" — the word "methodology" is more honest about what's shipped (docs, not code).

## URL field

`https://github.com/Korner83/ai-development-methodology`

## Text field (the body of the post)

A self-contained methodology for running software projects when some of your contributors are AI agents. Markdown + git only. No SaaS, no signup. CC BY 4.0.

Origin: I needed a way to keep my own project from collapsing under the weight of multiple AI agents working in parallel (two of them happened to grab the same auth-middleware task at 2am once). The methodology started as the project's `docs/methodology/` folder and grew into something portable.

What's in the repo:

- **13 short methodology docs** covering the four planning layers (strategy → pillars → epics → items), three discipline overlays (working principles, definition of done, lessons-learned memory), file-based locks for parallel contributors, git workflow, testing, human-roles, and milestone evaluation.
- **5 templates** (CLAUDE.md, AGENTS.md, AGENT_KICKOFF.md, AUTONOMOUS_LOOP.md, PROJECT_STRUCTURE.md) — paste-and-adapt for new projects.
- **`examples/`** — a fictional `tinker` (developer-notes CLI) project showing the methodology end-to-end.
- **`self-development/`** — the methodology applied to its own development as a meta worked example. The first semi-annual self-evaluation cycle just shipped today (v1.14.0 + v1.15.0 + v1.16.0).
- **CHEATSHEET.md** — one-page reference (~80 lines).

What's different from other approaches I've seen:

- **Tier matrix for autonomous loops** — instead of "AI can never touch the spec" or "AI can do whatever," it tiers proposed changes by risk (T0 cosmetic / T1 surgical / T2 substantive / T3 architectural), with T0/T1 auto-patched via cross-AI diff-verification on patch branches, T2/T3 deferred to human authorship.
- **Periodic deep-eval** — every Nth loop iteration, the project is scored on a 0–10 rubric per area (UX, security, performance, content quality, etc., adapted per project) against the next milestone's readiness criteria. Catches the "all items green, product unfit to ship" failure that per-item DoD misses.
- **Unsolvable issues are first-class** — handle / postpone / mark rather than forcing fixes that make things worse. The methodology explicitly disallows the "let's try one more refactor" anti-pattern.

I don't claim it's the best methodology. It's what worked for one real production project (a location-based audio app called WayWhisper) and one meta project (the methodology itself). I'd love to hear from anyone who tries it on a different shape of project — especially failures of the tier matrix or the rubric, which I haven't been able to stress-test with multiple adopters yet.

Repo: https://github.com/Korner83/ai-development-methodology
Cheatsheet: https://github.com/Korner83/ai-development-methodology/blob/main/CHEATSHEET.md

---

## What to expect in comments

HN comments on dev-methodology Show HN posts typically split into three camps:

1. **"This is just GitHub issues with extra steps"** — true and not-true. The response is that GitHub issues alone don't give you the planning cascade (strategy → pillars → epics → items) or the tier-matrix autonomy split for AI agents. Acknowledge the parallel.
2. **"You're describing what good engineering looks like"** — somewhat true. The response is that "good engineering" is exactly what the methodology operationalizes for AI-assisted projects where the implicit conventions break down at AI velocity.
3. **"Why not [SaaS tool X]?"** — typically Linear, Notion, Confluence, etc. The response is that the methodology is markdown + git on purpose — no vendor lock-in, no monthly cost, no data leaving your repo.

Don't engage with hostile commenters. Engage substantively with technical critique. Respond to the most-upvoted critical comment within a few hours of posting.

## Posting timing

- **Best:** Tuesday or Wednesday, 9–11 AM US Pacific (peaks European morning + US workday).
- **Worst:** Friday afternoon, Sunday, holidays.
- **One shot:** HN heavily penalizes reposts. Post once; if it doesn't get traction, don't repost the same URL.

## After posting

- Watch the post for the first 60 minutes; comments early shape the thread.
- The "second comment" trick: HN often rewards a substantive follow-up comment from the OP about a detail that wasn't in the post.
- Bookmark the comment URLs that contain critical feedback for the FEEDBACK.md inbox (per `methodology/12`).
