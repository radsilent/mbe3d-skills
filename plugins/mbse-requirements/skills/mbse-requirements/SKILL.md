---
name: mbse-requirements
description: Author, review, and repair system requirements to aerospace/defense standards. Use when writing or fixing requirements, applying EARS patterns, assigning requirement IDs, setting priority/verification method, splitting compound requirements, removing ambiguity, or reviewing a requirements document for quality. Triggers on requirement, shall statement, EARS, spec review, acceptance criteria, requirements quality, ReqIF.
---

# Requirements Authoring

Write requirements that survive a design review, an auditor, and a verification campaign.
Works on plain files. If an MBE3Dstudio server is configured, `mbe3d-load` pushes the
result into the live graph — but never block on the server; author first, load second.

## The five EARS patterns

Every requirement matches exactly one. If it matches none, it is not yet a requirement.

| Pattern | Template | Use for |
|---|---|---|
| Ubiquitous | `The <system> shall <response>.` | Always-true properties |
| Event-driven | `When <trigger>, the <system> shall <response>.` | Discrete stimulus |
| State-driven | `While <state>, the <system> shall <response>.` | Sustained mode |
| Unwanted behavior | `If <condition>, then the <system> shall <response>.` | Faults, off-nominal |
| Optional feature | `Where <feature is included>, the <system> shall <response>.` | Variants, options |

Complex requirements nest a state inside an event: `While <state>, when <trigger>, the
<system> shall <response>.` Nest no deeper than that — deeper nesting means you are
holding two requirements in one.

## Non-negotiables

1. **One shall per requirement.** "and", "or", a comma list, or a second sentence means split it.
2. **Named subject.** `The Perception Subsystem shall…`, never "the system" when a
   subsystem owns it and never "it".
3. **Measurable response.** Every performance claim carries a number, a unit, and a
   condition of measurement. `≤ 100 ms (95th percentile, measured sensor-frame-capture
   to track-publish, at 30 fps input)` — not "fast" or "in real time".
4. **No design in a requirement.** Requirements state *what* and *how well*. If it names
   a part number, an algorithm, or a data structure, it is a design decision — move it to
   a design element and derive the requirement above it. Exception: an interface
   requirement may name the interface it must conform to.
5. **No solution-free rationale gaps.** Every requirement gets a `rationale` — the reason
   it exists. A requirement nobody can justify is a requirement you delete.
6. **Verifiable as written.** Ask: *what test would fail this?* If you cannot name one,
   rewrite until you can. See `mbse-verification`.

## Banned words

Reject these on sight and rewrite: *user-friendly, robust, efficient, sufficient,
adequate, appropriate, as required, if practical, minimize, maximize, optimize, support,
handle, process, manage, etc., and/or, TBD (without an owner and a due date), quickly,
approximately (without a tolerance), state-of-the-art, seamless.*

`should`, `will`, `may` are not requirements. `shall` = binding requirement. `will` =
statement of fact about the environment. `should` = goal. Keep them in separate sections.

## Required fields

Every requirement carries at minimum:

```yaml
req_id: REQ-PERC-002          # stable, human, never reused (see ID scheme below)
name: Detection latency
text: "When a frame is received, the Perception Subsystem shall publish a track list within 100 ms (95th pct)."
requirement_type: Functional   # Functional | Performance | Interface | Safety | Security | Environmental | Regulatory
priority: Critical             # Low | Medium | High | Critical  (PascalCase — enums are case-sensitive downstream)
verification_method: Test      # Test | Analysis | Demonstration | Inspection | Simulation
rationale: "Bounds the control loop's sense-to-act budget of 250 ms."
derived_from: [REQ-SYS-014]    # parent(s)
allocated_to: [Perception]     # owning component
status: Proposed               # Proposed | Approved | Implemented | Verified | Rejected
```

## ID scheme

`REQ-<SUBSYSTEM>-<NNN>`, safety requirements `SR-<SUBSYSTEM>-<NNN>`, hazards `HAZ-<NNN>`,
verifications `VER-<NNN>`, interfaces `ICD-<NNN>`. Three digits, zero-padded, allocated
sequentially per subsystem. **IDs are permanent.** Deleting a requirement retires its ID;
never reissue it. When a requirement is split, retire the parent and issue two new IDs,
with `derived_from` pointing back at the retired one so the history survives.

## Review checklist

Run this over any requirement set you are handed:

- [ ] Each requirement matches one EARS pattern
- [ ] One `shall` each; no compound requirements
- [ ] Every performance number has units + measurement conditions
- [ ] No banned words
- [ ] No design leakage
- [ ] Every requirement has `rationale`, `verification_method`, `priority`
- [ ] Every requirement traces up (`derived_from`) and down (`verified_by`) — see `mbse-traceability`
- [ ] No duplicate requirements (same intent, different words) — search by meaning, not by string
- [ ] No orphan TBDs
- [ ] Priorities are defensible: `Critical` means loss of mission/life/certification, not "the customer asked twice"

## Workflow: repairing a bad requirement

1. Quote the original verbatim.
2. Name the defects against the checklist above.
3. Emit the rewrite in EARS form with all required fields.
4. If the original was compound, emit N requirements and state the ID retirement.
5. State the verification that would fail it.

Never silently improve a requirement — the diff is the deliverable, because someone has
to approve the change.
