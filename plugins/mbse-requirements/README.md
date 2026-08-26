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
| `mbe3d-connect` | Connecting to an MBE3Dstudio server, and its six documented failure modes |
| `mbe3d-load` | Getting a model in with your engineering attributes intact |
| `mbe3d-analyze` | SPARQL over the real vocabulary, competency suites, CI gates |
| `mbe3d-studio` | The 3D surface and the provenance model underneath it |

Five of the nine work on plain files with nothing installed. Four need an
MBE3Dstudio server.

## Licence

Free to use, not to repackage. See [LICENSE.md](LICENSE.md).
