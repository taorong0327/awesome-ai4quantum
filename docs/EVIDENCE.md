# Evidence Policy

This repository distinguishes a research direction's promise from the evidence that currently supports it. It covers classical AI/ML for quantum-hardware reliability and fault-tolerant computing.

## Admission rubric

Each entry is assessed against the following dimensions.

| Dimension | Maximum | What counts |
|---|---:|---|
| Engineering impact | 3 | Explicit change in logical error, deadline/latency, fidelity/yield, calibration time, or fault-tolerant resource cost. |
| Evidence maturity | 3 | Hardware plus peer review is strongest; rigorous simulation and theory are useful but separately labeled. |
| Reproducibility | 2 | Public code, data, workload, noise model, and evaluation protocol. |
| Operational fit | 2 | Reports deployment cost, drift/OOD behavior, latency, memory, training cost, or cross-code/device generalization. |

This rubric guides editorial judgment; it is not published as a spurious numerical leaderboard.

## Editorial placement

- **Core research map** — peer-reviewed work with a clear engineering target plus either meaningful hardware/system validation or a runnable public artifact with a defined evaluation contract.
- **Frontier watchlist** — credible, falsifiable directions whose evidence remains incomplete, narrowly scoped, or untested under the relevant deployment contract.
- **Cross-cutting infrastructure** — benchmarks, data, simulators, and tools that enable research but are not themselves promoted as a research direction.
- **Adjacent fields** — useful techniques outside the core scope, such as NISQ error mitigation or generic circuit synthesis.

## Required distinctions

Every research entry should make these distinctions when relevant:

```text
[peer-reviewed | preprint]
[hardware | simulation | theory]
[public-data | data-restricted]
[open-code | code-closed | public-artifact | industry-artifact]
[latency-reported]
[benchmark | supporting-tool | historical-precursor]
```

Multiple evaluation-setting tags may apply. Omit a tag when its status is unknown; do not use a negative tag such as `latency-not-reported` merely because a source does not foreground it. “Hardware” does not imply that code, workloads, or raw data are public. “Open code” does not imply an independent reproduction. “SOTA” is avoided unless the comparison contract is explicit and relevant to the claimed use case.

## Scope boundary: QEC and QEM

Fault-tolerant QEC provides scalable logical protection through error-correcting codes and fault-tolerant operations. Quantum error mitigation uses additional sampling and post-processing to estimate ideal results from noisy executions. It can coexist with QEC, but is not itself the route to scalable fault-tolerant protection; AI-assisted QEM is therefore kept in the adjacent section rather than silently merged into the QEC core.
