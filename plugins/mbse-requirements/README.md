# MBSE Requirements Authoring

A Claude Code skill that teaches your agent to write requirements that survive a
design review.

Your agent already writes code. Ask it for requirements and what comes back is
compound `shall` statements, performance claims with no units or measurement
conditions, and design decisions dressed up as requirements. It reads well
enough to circulate, which is the problem — you find out in review, and review
is expensive.

This skill covers:

- the five EARS patterns, and which one a given requirement wants;
- permanent ID schemes that survive renumbering;
- a banned-word list that rejects "robust", "user-friendly" and the rest on
  sight, with the reason attached;
- splitting compound requirements without losing intent;
- a repair workflow that shows you the diff rather than silently rewriting your
  specification.

And, for reviewing a set rather than writing one — where the expensive findings
actually are:

- a conflict sweep that catches the same quantity carrying two different values
  in two different documents, which is the defect that survives every
  per-requirement check because both halves look correct alone;
- window arithmetic, so "99.95 % uptime during the event" gets multiplied out to
  the 5.4 seconds it actually permits before anyone commits to it;
- budget closure, checking that the children sum under the parent *and* that the
  parent's measurement window is the one the budget measures;
- coverage matrices driven from the hazard log and anchor catalog inward, because
  a missing safety requirement is invisible from inside the requirements file;
- a disposition ledger for the re-review, which separates "closed" from "closed
  on an assumption I made and you have not confirmed".

## Install

```
/plugin marketplace add radsilent/mbe3d-skills
/plugin install mbse-requirements@vector-stream-systems
```

## The other eight

This is one skill of nine. The rest are in the
[MBE3D Systems Engineering Skill Pack](https://vectorstreamsystems.com/skillpack),
a one-time purchase:

| | |
|---|---|
| `mbse-safety-analysis` | MIL-STD-882E severity, probability and RAC matrix, FHA guide words, FMEA, mitigation order of precedence |
| `mbse-traceability` | Six audit queries for unverified requirements, orphans, unmitigated hazards and dead tests, plus change-impact analysis |
| `mbse-verification` | Method selection, machine-evaluable pass criteria, evidence schema for ML and autonomy metrics |
| `mbse-model-format` | A portable, diffable `.mbse.json` model file with a validator |
| `mbe3d-connect` | Connecting to an MBEstudio server, and its six documented failure modes |
| `mbe3d-load` | Getting a model in with your engineering attributes intact |
| `mbe3d-analyze` | SPARQL over the real vocabulary, competency suites, CI gates |
| `mbe3d-studio` | The 3D surface and the provenance model underneath it |

Five of the nine work on plain files with nothing installed. The other four need
an MBEstudio server.

## Licence

MIT. See [LICENSE](LICENSE). Use it, change it and redistribute it, as long as
the copyright and licence notice stay with it.

The MIT licence covers this skill as published in this repository. The other
eight skills in the pack, and the pack's own copy of this one, are sold under a
separate licence: https://vectorstreamsystems.com/skillpack

Its guidance on MIL-STD-882E, ARP4761, DO-178C and ISO 26262 is a working
summary. It is not a substitute for the standards as issued, for a certified
process, or for a qualified engineer.

Questions: streamline@vectorstreamsystems.com
