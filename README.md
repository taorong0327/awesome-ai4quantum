# Awesome AI for Quantum Hardware & Fault-Tolerant Computing

> A curated, evidence-tagged map of **classical AI/ML for quantum-hardware reliability and fault-tolerant computing** — QPU characterization and control, decoder engineering, adaptive QEC operations, and resource-aware fault-tolerant optimization.

**This is not a Quantum Machine Learning (QML) list.** It does not collect quantum neural networks or quantum algorithms intended to accelerate classical machine learning.

The organizing unit is an engineering task, not an AI method, vendor, or paper format. This list favors work that changes an explicit quantum-engineering metric — logical error rate, deadline compliance, stability under drift, calibration yield, or fault-tolerant resource cost — and makes the evidence visible.

## Contents

- [How to read this list](#how-to-read-this-list)
- [Core research map](#core-research-map)
  - [1. QEC decoder systems](#1-qec-decoder-systems)
  - [2. Adaptive QEC operations](#2-adaptive-qec-operations)
  - [3. QPU reliability modelling, characterization, and calibration](#3-qpu-reliability-modelling-characterization-and-calibration)
  - [4. Fault-tolerant resource optimization](#4-fault-tolerant-resource-optimization)
- [Cross-cutting infrastructure](#cross-cutting-infrastructure)
- [Frontier watchlist (updated September 2026)](#frontier-watchlist-updated-september-2026)
- [Adjacent fields](#adjacent-fields)
- [Contributing](#contributing)
- [License](#license)

## How to read this list

### Map logic

| Research task | What is being improved | The claim that must eventually be tested |
|---|---|---|
| QEC decoder systems | Syndrome-to-correction inference | Logical error **and** deadline/throughput under an explicit noise and workload model |
| Adaptive QEC operations | Decoder, calibration, or control updates from measurement history | Recovery from drift or non-stationarity without destabilizing the QEC experiment |
| QPU reliability | Models and actions for characterization, calibration, and control | Calibration yield, fidelity/stability, time-to-tune, or downstream QEC benefit |
| Fault-tolerant resource optimization | Verified logical circuits and their physical-resource cost | T count, qubits, spacetime volume, or another explicit fault-tolerant resource metric |

Tools, simulators, data, and benchmarks are indexed as **horizontal infrastructure**. They are useful enablers, but not research directions equal to the four task layers above.

### Scope and editorial rule

An item enters a **core** section only when it has a clear engineering target and meets the admission threshold in the [Evidence Policy](docs/EVIDENCE.md): a peer-reviewed result plus either meaningful hardware/system validation or a runnable public artifact with a defined evaluation contract. `Frontier` is deliberately different: it contains promising directions with a falsifiable next test, not declared winners.

### Evidence tags

- `[peer-reviewed]` / `[preprint]` — publication maturity.
- `[hardware]`, `[simulation]`, or `[theory]` — evaluation setting; more than one may apply.
- `[public-data]` / `[data-restricted]`, `[open-code]` / `[code-closed]`, `[public-artifact]`, or `[industry-artifact]` — data and implementation accessibility.
- `[latency-reported]` — the source reports a timing or throughput result relevant to deployment.
- `[benchmark]`, `[supporting-tool]`, and `[historical-precursor]` — editorial context, not quality rankings.

Unknown status is omitted rather than guessed. For the detailed admission and labeling policy, see [Evidence Policy](docs/EVIDENCE.md).

## Core research map

### 1. QEC decoder systems

#### Device-conditioned decoding

- [Learning high-accuracy error decoding for quantum processors (AlphaQubit)](https://www.nature.com/articles/s41586-024-08148-8) — A recurrent-transformer decoder that uses Sycamore syndrome data and soft-readout/leakage information; its distance-3–11 simulations additionally model crosstalk. It beats the reported tensor-network baseline on distance-3 and distance-5 hardware data. Its distance-11 result is realistic-noise simulation, not a large-QPU demonstration. `[2024] [peer-reviewed] [hardware] [simulation] [public-data]`
- [Optimization of decoder priors for accurate quantum error correction](https://doi.org/10.1103/PhysRevLett.133.150603) — Calibrates hardware-informed decoder priors with an RL-inspired method in repetition- and surface-code memory experiments on Google’s Sycamore processor, bridging fixed analytic priors and device-adapted decoding. `[2024] [peer-reviewed] [hardware]`
- [A fault-tolerant neutral-atom architecture for universal quantum computation](https://doi.org/10.1038/s41586-025-09848-5) — A cross-platform system case study that includes loss-aware ML decoding on a 448-atom neutral-atom platform. Its distance- and circuit-specific training limits remain explicit. `[2026] [peer-reviewed] [hardware]`

#### Beyond memory experiments

- [Learning to decode logical circuits (MCCD)](https://www.nature.com/articles/s43588-025-00897-4) — A modular, data-centric decoder for logical circuits with entangling operations; it moves the target from memory experiments to correlated logical workloads. `[2025] [peer-reviewed] [simulation] [open-code]`
- [Machine learning message-passing for scalable QLDPC decoding (Astra)](https://www.nature.com/articles/s41534-025-01033-w) — A graph-native learned message-passing decoder for surface and bivariate-bicycle codes that extrapolates from lower to larger code distances. It is strategic, but remains simulation-first rather than hardware-validated. `[2025] [peer-reviewed] [simulation] [open-code]`

#### Real-time deployment and evaluation gap

- [Quantum error correction below the surface code threshold](https://www.nature.com/articles/s41586-024-08449-y) — A system landmark for below-threshold QEC on Willow. It is also an essential cautionary reference: its high-accuracy neural decoder is an offline path, whereas the real-time decoder is a Sparse Blossom streaming stack. Accuracy and deadline compliance must be evaluated separately. `[2025] [peer-reviewed] [hardware] [public-data] [latency-reported]`

### 2. Adaptive QEC operations

This section covers systems that use QEC measurements to adapt a decoder, calibration, or control policy **across repeated experimental runs**. It is distinct from improving a static decoder on a fixed noise model.

- [Real-time quantum error correction beyond break-even](https://doi.org/10.1038/s41586-023-05782-6) — A historical precursor: model-free reinforcement learning optimized bosonic-QEC control and achieved a reported logical-coherence gain beyond break-even. `[2023] [peer-reviewed] [hardware] [historical-precursor]`
- [Realizing a deep reinforcement learning agent for real-time quantum feedback](https://www.nature.com/articles/s41467-023-42901-3) — Demonstrates direct-on-experiment RL training and sub-microsecond FPGA feedback for a superconducting qubit. It is a control precursor, rather than a full QEC system. `[2023] [peer-reviewed] [hardware] [latency-reported] [historical-precursor]`
- [Reinforcement learning control of quantum error correction](https://www.nature.com/articles/s41586-026-10759-2) — Uses detection events as a learning signal to steer more than 1,000 QEC control parameters on Willow under drift. This is the clearest hardware evidence for closed-loop adaptive QEC; [public data](https://doi.org/10.5281/zenodo.17566521) are available, but code is proprietary and steering within a single long logical computation remains open. `[2026] [peer-reviewed] [hardware] [public-data] [code-closed]`

### 3. QPU reliability modelling, characterization, and calibration

This is deliberately **not** called “error mitigation.” The scope is learning hardware behavior that improves characterization, calibration, decoder adaptation, or compiler decisions.

- [Robustly learning the Hamiltonian dynamics of a superconducting quantum processor](https://www.nature.com/articles/s41467-024-52629-3) — Structure-exploiting learning identifies Hamiltonian dynamics on up to 14 sites of a Sycamore superconducting processor and diagnoses implementation deviations. `[2024] [peer-reviewed] [hardware]`
- [Fully autonomous tuning of a spin qubit](https://www.nature.com/articles/s41928-025-01562-4) — A full hardware-tuning workflow combining learned classifiers, Bayesian optimization, and experimental feedback. It is a device-engineering result, not evidence that generic LLMs autonomously operate large QEC systems. `[2026] [peer-reviewed] [hardware] [open-code] [public-data]`

### 4. Fault-tolerant resource optimization

This deliberately narrow section includes work whose target is an explicit fault-tolerant resource metric, not generic circuit optimization alone.

- [Quantum circuit discovery for fault-tolerant logical state preparation with reinforcement learning](https://doi.org/10.1103/gqpr-dgz7) — A reinforcement-learning system for finding compact, hardware-constrained logical state-preparation circuits. Its targets are fault-tolerant and verification-based; hardware implementation remains future work. `[2025] [peer-reviewed] [simulation] [open-code]`
- [Quantum circuit optimization with AlphaTensor-Quantum](https://www.nature.com/articles/s42256-025-01001-1) — A landmark for fault-tolerant T-count optimization: reinforcement learning plus tensor decomposition, explicit resource metrics, released code/data, and correctness checks. It is not a general zero-cost compiler; compute and generalization costs remain part of the result. `[2025] [peer-reviewed] [simulation] [open-code] [public-data]`

## Cross-cutting infrastructure

Infrastructure is indexed here for practical use. It is not presented as a research direction equal to QEC, QPU operation, or fault-tolerant resource optimization.

### Benchmarks and evaluation contracts

- [decoder-bench](https://github.com/satvikmaurya/decoder-bench) — Dataset-generation and evaluation tooling for comparing QEC decoders across codes, noise models, and memory or surface-code lattice-surgery workloads. `[2025] [benchmark] [open-code] [public-data]`
- [QEC LEGO Bench](https://qec-lego-bench.readthedocs.io/en/latest/) — Composable benchmark and experiment infrastructure for QEC decoding. `[benchmark] [open-code]`
- [StabilizerBench](https://arxiv.org/abs/2604.21287) — A 2026 benchmark for AI-assisted QEC circuit synthesis; useful as a Frontier evaluator, not yet a mature deployment result. `[2026] [preprint] [benchmark]`

### Public QEC data

- [Sycamore QEC data for AlphaQubit](https://doi.org/10.5281/zenodo.6804040) — Experimental data supporting device-conditioned neural decoding. `[public-data]`
- [Willow below-threshold QEC data](https://doi.org/10.5281/zenodo.13273331) — Experimental data accompanying below-threshold surface-code QEC. `[public-data]`
- [Willow RL-control QEC data](https://doi.org/10.5281/zenodo.17566521) — Detection-event and control data for closed-loop QEC experiments. `[public-data]`

### Simulators, decoders, and supporting toolchains

- [Stim](https://github.com/quantumlib/Stim) — Fast stabilizer-circuit simulation for decoder data generation and evaluation. `[open-code] [supporting-tool]`
- [PyMatching](https://github.com/oscarhiggott/PyMatching) — Minimum-weight-perfect-matching decoder implementation and baseline. `[open-code] [supporting-tool]`
- [Sinter](https://github.com/quantumlib/Stim/tree/main/glue/sample) — Sampling and statistical-analysis tooling distributed with Stim. `[open-code] [supporting-tool]`
- [CUDA-Q QEC](https://developer.nvidia.com/cuda-q-qec) — GPU-oriented QEC simulation and decoder-deployment tooling. It is infrastructure, not a stand-alone AI research claim. `[industry-artifact] [supporting-tool]`
- [Ising Decoding](https://github.com/NVIDIA/Ising-Decoding) — Open NVIDIA training recipes for AI QEC decoder predecoding: a neural network consumes detector syndromes before a standard global decoder produces the final logical decision. Treat it as an engineering artifact, not an independently validated academic SOTA claim. `[open-code] [industry-artifact] [simulation] [supporting-tool]`

## Frontier watchlist (updated September 2026)

These are testable forecasts, not core claims. A direction moves into the core only when it obtains stronger workload, latency, reproducibility, or hardware evidence.

- **Non-stationary, calibration-shift-aware decoding** — Evaluate recovery from drift, leakage, correlated bursts, and distribution shift rather than fixed i.i.d. Pauli noise alone.
- **Hybrid learned + structured real-time decoders** — Learned predecoders, residual matching, distillation, quantization, and FPGA/GPU/ASIC deployment should be judged by end-to-end p50/p99 latency, backlog, and QPU logical error rate.
- **Dynamic logical workloads** — Extend decoder tests beyond memory to entangling logical circuits, lattice surgery, magic-state protocols, and code deformation. Lattice surgery remains Frontier rather than an established AI-decoding result.
- **QLDPC and graph-native learned decoding** — Strategic because of resource-efficient code families, but current learned-decoder evidence is primarily simulation; circuit-level noise, latency, and hardware data are the next thresholds.
- **Auditable autonomous laboratory workflows** — [An agent-based laboratory framework](https://doi.org/10.1016/j.patter.2025.101372), demonstrated on a three-qubit subset of a 16-qubit superconducting platform, and [QCalEval](https://arxiv.org/abs/2604.25884) are promising only when safety constraints, recovery rates, versioned experimental traces, and end-to-end gains are measured. A small hardware demonstration or an agent benchmark alone is not closed-loop-QPU proof.

## Adjacent fields

### AI-assisted quantum error mitigation (NISQ / pre-fault-tolerance)

Fault-tolerant QEC provides scalable logical protection through error-correcting codes and fault-tolerant operations. Quantum error mitigation (QEM) uses additional sampling and post-processing to estimate ideal results from noisy executions; it can coexist with QEC, but is not itself the route to scalable fault-tolerant protection. QEM is therefore adjacent rather than a core section of this repository.

- [Machine learning for practical quantum error mitigation](https://www.nature.com/articles/s42256-024-00927-2) — ML-QEM demonstrated on IBM hardware with code and data release. `[2024] [peer-reviewed] [hardware] [open-code] [public-data]`
- [Exponentially tighter bounds on limitations of quantum error mitigation](https://www.nature.com/articles/s41567-024-02536-7) — A critical theoretical counterweight: generic QEM can require prohibitive sampling overhead. `[2024] [peer-reviewed] [theory]`

### General AI circuit synthesis and transpilation

These are useful adjacent techniques, but their present evaluation targets are generic logical/NISQ circuit tasks rather than an explicit fault-tolerant resource objective.

- [QSeed: Improving quantum circuit synthesis with machine learning](https://doi.org/10.1109/QCE57702.2023.00093) — Learns useful seeds for unitary synthesis to improve search speed while retaining low gate counts. `[2023] [peer-reviewed] [simulation]`
- [Quarl: A learning-based quantum circuit optimizer](https://doi.org/10.1145/3649831) — Uses GNN representations and reinforcement learning to select semantics-preserving circuit rewrites, with a public experimental artifact. `[2024] [peer-reviewed] [simulation] [public-artifact]`
- [Practical and efficient quantum circuit synthesis and transpiling with reinforcement learning](https://arxiv.org/abs/2405.13196) — A hardware-aware RL transpilation direction with an implementation path in the [Qiskit AI Transpiler](https://github.com/Qiskit/qiskit-ibm-transpiler). Treat it as a product-integrated engineering signal pending broader independent validation. `[2024] [preprint] [open-code] [industry-artifact]`
- [QCircuitBench](https://proceedings.neurips.cc/paper_files/paper/2025/hash/3e343c7fa87656d7e88e9a83cb2a5d10-Abstract-Datasets_and_Benchmarks_Track.html) — An executable benchmark for quantum algorithm and circuit design, with syntax, semantic, and efficiency checks rather than LLM-as-judge evaluation. `[2025] [peer-reviewed] [benchmark] [public-data]`

### Related lists

- [Awesome Quantum Machine Learning](https://github.com/artix41/awesome-quantum-ml) — Quantum computers for machine learning; intentionally outside this repository's scope.
- [Awesome Quantum Software](https://github.com/qosf/awesome-quantum-software) — Broad quantum-software catalogue.
- [ML4QTech Collection](https://github.com/ML4QTech/Collection) — Broader ML-for-quantum-science community collection.

## Contributing

Contributions are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) and include a primary source, a neutral description, evidence tags, artifact status, and the exact workload or noise setting.

## License

[MIT](LICENSE) © Rong Tao
