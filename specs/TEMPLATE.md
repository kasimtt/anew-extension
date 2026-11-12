# Spec NNNN — <short name>
<!-- Small behavior changes use TEMPLATE-mini.md — brevity is sanctioned, discipline is not. -->
<!-- Write the content in the document language from AGENTS.md. Headings, field labels and Status
     values stay English: scripts/doctor and the segment entry checks read them. -->

- Status: Draft | Approved | In progress | Shipped
  <!-- State machine (who moves it): Draft → Approved (human approval, end of /analyze)
       → In progress (Developer, when /build starts) → Shipped (human, at ship, when the file
       moves to specs/done/). /plan refuses to run unless the status is Approved. -->
- Mode: lite | strict (from AGENTS.md at creation time)
- Plan: `specs/plans/NNNN-plan.md`
- Self-critique: pending
  <!-- done | pending (<condition>) — "done" once the human approved the self-critique gaps
       (prompts/spec.md); pending with its condition when deferred (e.g. "after 0012 ships").
       doctor: pending warns on a Draft (expected until approval) and is a gate past approval. -->
- Design: <!-- UI spec only (User experience is not "none") — the design artifact's address and the
       approved version: "<address> (<version label>)", or the dated export when the tool gives no
       version. No UI → "none — no user interface". Never a copy in the repo. (ANEW-F0001) -->
- Design approved by / on: —
  <!-- UI spec only — "<name>, <YYYY-MM-DD>", written at the design gate, which comes BEFORE spec
       approval (workflows/segments.md, ANALYZE). doctor: past approval, a UI spec without the
       address or this record is a gate. -->

## Intent
<!-- 3–5 sentences, BUSINESS language: who wants this and why; what success looks like;
what is deliberately NOT being done. Decisions from clarifying questions are folded in here. -->

## Requirements
<!-- Behavior, not technical solutions. No endpoints, tables, or caches here — the plan owns "how". -->

## User experience
<!-- Required heading; no UI → write "none — no user interface". The behavior as the user sees it,
     not visual polish:
     - Flow: the steps a user takes, entry point → outcome.
     - States: every state of each screen — empty, loading, error, success, no permission.
     - Design: the Analyst draws a design artifact from this section (prompts/spec.md) — one
       artboard per screen × state listed here, each labelled with the criteria it serves
       (e.g. "List · empty — AC-2"); its address goes in the `Design:` field above, never a
       copy in the repo (docs/testing.md, Evidence policy).
     - Accessibility: keyboard path, labels, contrast expectations.
     Every state listed here gets an acceptance criterion below. -->

## Constraints & out of scope
<!-- Hard limits (performance targets, compliance) and conscious V1 exclusions. -->

## Acceptance criteria
<!-- Each line independently testable. Cover the happy path, boundaries, empties, and error cases.
     More than one user capability or ~8–10 criteria → propose a split (prompts/spec.md, SIZE).
     Moved out at the ship gate (never a waiver; workflows/feature-development.md step 10): keep
     the line, on that same line: - [ ] ~~AC-n — …~~ → moved to B-<n> | spec <NNNN> — <name>,
     <YYYY-MM-DD>, <why>. doctor checks it on every new ship; a sensitive-area criterion stays. -->
- [ ] AC-1 —
- [ ] AC-2 —
- [ ] AC-3 —

## Definition of Done
- [ ] Every acceptance criterion mapped to proof (test or reproducible observation)
- [ ] `scripts/check` green
- [ ] Independent review done; real findings fixed, noise rejected with written rationale, deferred ones in `specs/backlog.md`
- [ ] Docs / ADRs updated if behavior or architecture changed
- [ ] Spec moved to `specs/done/` (it becomes immutable there)

## Scorecard (fill at ship — honest numbers make the process improvable)
| Metric | Value |
|---|---|
| Spec revisions | |
| Fix rounds | |
| Review findings: real / noise / deferred | |
| Regressions introduced | |
| Bugs escaped to production | |
