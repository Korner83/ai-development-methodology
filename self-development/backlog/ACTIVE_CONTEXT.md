# ACTIVE_CONTEXT.md — volatile working state

**Baton, not journal.** Where the current session is, so the next one — or this one after a
context reset — can resume without re-deriving state from scratch. Per
[`methodology/08_lessons_and_memory.md` "Active context"](../../methodology/08_lessons_and_memory.md#active-context-the-volatile-working-file):
written *before* a context reset, read *first* on resume, then **verified against live `git log`
and item state**, which are authoritative when they disagree with this file.

Overwritten, not appended. The durable record lives in commits, `ARCHIVE.md`, and memory.
If a line here is worth keeping, it belongs in one of those instead.

_Last updated: 2026-08-19 — after E08 closed (v1.30.0)._

## Current focus

Nothing in flight. **No active epic**, no open items in any epic, working tree clean.

## Recent changes (this session)

- **v1.30.0**: E08 chartered → executed → closed. Four items:
  - **BL-0030** `templates/ROLE_BRIEFS.md` (new, 197 lines) — six paste-able per-phase briefs for
    the phases that had rules but no prompt. Briefs link to their rules doc and restate nothing.
  - **BL-0031** wired it into `README.md`, `00_README.md`, and both existing prompt templates;
    closed E07's open question in the charter *and* in E07's `FUTURE.md`.
  - **BL-0032** blast radius as a seventh required verification dimension in `10`.
  - **BL-0033** the unattended-mode caution in both `AUTONOMOUS_LOOP.md` files.
- **README table capped.** The 21-row problem/solution table moved to `methodology/00_README.md`
  (where it replaced a stale five-bullet subset of itself); the README keeps 12 rows plus a link.
  374 → 333 → **331**. The growth mechanism is now closed, not just the symptom — policy recorded
  in `P2_doc_clarity.md`.
- **Staleness swept** in `backlog/README.md` (epic tree still said `01-` … `05-cheatsheet`, ID
  space said "starts at BL-0001", status section still described the bootstrap as in progress) and
  `E04/BACKLOG.md` (said `planned`, is `parked — will not resume`).

## Next steps

The backlog is not the binding constraint — the milestone is.

1. **The distribution drafts were deleted (2026-08-19), by decision.** Maintainer position: a
   good project sells itself. The four staged drafts are gone and are **not recoverable** — the
   folder was gitignored, so no commit contains them. What this does *not* change: P5 stays at
   6/10 and closed beta stays **NOT READY**. Adoption now rests on passive channels only
   (GitHub search and topics, Pages, the awesome-list listings). `HUMAN_NEEDED.md` is empty.
   Expect a long quiet period before any adopter signal, if one comes.
2. **The backlog is empty** — zero active, zero planned. Chartering is a deliberate act; the loop
   should halt and surface rather than promoting anything itself.
3. **Four Tier-2 deferrals** remain in
   [E06's FUTURE.md](epics/E06-bmad-v6-landscape-pass/FUTURE.md). Three further findings are held
   with reasoning in [E08's charter](epics/E08-role-briefs/README.md#out-of-scope) — two-level
   acceptance criteria, chronological task ordering, spec/plan artifact split.
4. **Semi-annual self-evaluation due 2026-11-25** — it should check whether the **v1.25.0–v1.30.0**
   conventions are actually being used or have become dead text. Three landscape passes and a
   dozen-plus conventions have now shipped with zero external adopters exercising any of them.
5. **A second example project** (web-app / database / small-team shaped) is a known gap and is
   deliberately **not** chartered: its shape should come from adopter signal, not a guess.

## Watch out for

- **Check `origin/main` before branching.** An earlier session lost time to a stale local `main`.
- **The version number is claimed in seven places**, not four: `README.md` badge plus three prose
  lines, `CHEATSHEET.md` pin, `STATUS.md`, and the `CHANGELOG` heading. Grep for the old version
  rather than working from a list.
- **Line endings are mixed.** Most files are CRLF, but some (`backlog/README.md`,
  `E04/BACKLOG.md`) are LF-only, and `core.autocrlf=true` hides it. Any script that edits files
  must match per file or it produces a whole-file diff.
- **Do not build a `\x{...}` character into a byte-mode perl edit.** It upgrades the whole string
  and a following `utf8::encode` double-encodes every existing multi-byte character in the file.
  Cost this session: one file silently mojibaked and regenerated. Use raw UTF-8 byte sequences.
- **A link checker must model fenced blocks and inline code**, and must map each space in a
  heading to its own dash (`frozen intent — approved goals` → `frozen-intent--approved-goals`).
  Collapsing space runs produces ~100 false "broken anchors" and an unusable report.

## Not here on purpose

Durable lessons (the mixed-line-endings and slug-generation ones above are candidates for memory
entries), decisions with lasting force, and anything another session would need *after* this work
ships. Those go to `memory/`, the changelog, or the item body — not to a file that gets overwritten.
