---
description: "Segment ANALYZE: intent → clarify → spec → spec approval. Always stops at the handoff."
argument-hint: short feature description
---
Read AGENTS.md, docs/roles/analyst.md, and workflows/segments.md. Run the ANALYZE segment for:
$ARGUMENTS

Follow the segment contract exactly: entry check (no twin spec), prompts/clarify.md then
prompts/spec.md, the spec approval gate, set "Status: Approved", write the handoff, STOP.
Never produce a plan, a plan suggestion, or code.
Design artifact (UI spec, ANEW-F0001): draw it as a Claude Design artifact (Artifact type
"Design"), one artboard per screen × state; at design approval publish it with the label
`spec <NNNN> — approved` and write its address and that label in `- Design:`.
