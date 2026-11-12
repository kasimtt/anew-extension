# ANEW-F0001 — UI specs carry an approved design artifact

- Status: Accepted
- Date: 2026-11-12

## Context
ANEW-0008 put user experience into the spec but kept the design optional and outside ANEW: the
Analyst links a design if one exists and never invents visuals; there is no design gate. Teams
building internal software on this fork mostly have no separate design stage, so a UI spec is
approved as text and the first time anyone sees the screens is BUILD — where a misread layout is
expensive. ANEW-0008 names this exact signal as its revisit trigger: "Teams need design approval
as a separate human gate before ANALYZE ends."

## Decision
A spec with a user interface (its "User experience" is not `none — no user interface`; a
mini-spec that changes UI) carries a **design artifact** the Analyst draws from the analysis: one
artboard per screen × state the section lists, each labelled with the criteria it serves, at a
stable address and a fixed version. The spec records it in `Design:` and its approval in
`Design approved by / on:`. Design approval is its own gate message, asked **before** spec
approval; `Status: Approved` needs both. A design change after approval is a spec change (R-08).
The core names no tool (ANEW-0011); an adapter may name the tool it uses (ANEW-0001).
`scripts/doctor` validates the two fields (WARN locally, FAIL under `--strict`).

## Consequences
- Benefits: screens are seen and approved before the plan; VERIFY compares its screenshots with
  an approved version, state by state; the rule moves from Documented to Validated (ANEW-0004).
- Costs: ANALYZE is longer for UI work and has one more gate; the design lives outside the repo
  on a third-party service, so it must be shared with the approver, reviewer and QA, and a team
  must be allowed to keep its screen designs there. ANEW still cannot judge visual quality.
  doctor reads one more free-text section; unreadable means "has a UI" (fail-closed).

## Alternatives considered
- Keep ANEW-0008 as it is: rejected — the trigger it named has fired.
- A DESIGN segment with a Designer role: rejected for the reason ANEW-0008 gave — a new stage
  and role for what one more gate inside ANALYZE covers.
- Name a design tool in the core: rejected — against ANEW-0011; the adapter carries it.
- Number this ANEW-0013: rejected — upstream ANEW continues its own sequence; `ANEW-F` marks
  this fork's decisions and keeps upstream syncs free of number clashes (`.anew-dev/FORK.md`).

## Revisit triggers
- Approved designs repeatedly diverge from what ships (the version pinning is not working).
- A team's policy forbids keeping screen designs on the artifact service.
- Upstream ANEW takes a different design rule (reconcile on the next sync).
