# Awesome AI for Practical Quantum Computing ⚛️

<p align="center">
  <img src="assets/qec-chaos-mascot.png" width="560" alt="A lively quantum error-correction mascot with a syndrome graph, detector sparkle, lightning bolt, and checker tile." />
</p>

<p align="center">
</p>

> **The Mainline**
>
> `real-device noise & simulation → decoder systems → runtime deployment & adaptation`
>
>  **classical AI/ML for practical, fault-tolerant quantum systems**.
>
>  *what moves a QEC system from a model demo toward operation?*

## 🧭 Directory

- **[🏁 Mainline — hardware-adaptive QEC](#mainline)**
  - [🧪 Hardware: noise, data, and simulation](#hardware--noise-data-and-simulation)
  - [🧠 Decoder systems](#decoder-systems)
  - [⚡ Runtime and adaptive operation](#runtime-and-adaptive-operation)
- **[📡 Radar — what's new](#radar)** 
- **[🧩 Ecosystem — reproduce and tool](#ecosystem)**
- **[🛤 Parallel tracks](#parallel-tracks)** — adjacent but non-core research directions.
- [🌍 Related lists](#related-lists) · [🫶 Contributing](#contributing) · [📜 License](#license)

---

<a id="mainline"></a>

## 🏁 Mainline — hardware-adaptive QEC system maturation

> characterize or model the device → decode its syndromes → deploy and adapt.

```text
🧪 hardware layer: noise, data, simulation
                    ↓
🧠 decoder systems
                    ↓
⚡ runtime layer
```

<a id="hardware--noise-data-and-simulation"></a>

### 🧪 Hardware — noise, data, and simulation

What error process the decoder actually faces: leakage, crosstalk, readout effects, drift, and calibration context. Generic engines are indexed in the [Reproducibility Ecosystem](#reproducibility-ecosystem).

#### 🔬 Device characterization and calibration

- [Robustly learning the Hamiltonian dynamics of a superconducting quantum processor](https://www.nature.com/articles/s41467-024-52629-3) — Structure-exploiting learning estimates Hamiltonian dynamics from time-series data on up to 14 qubits of a Sycamore processor and diagnoses implementation deviations.<br>
  **Reproduction:** **hardware:** time-series measurements on up to 14 Sycamore qubits · experimental data and code are available from the authors on request; no public runnable artifact was located. `[2024] [hardware]`

- [Fully autonomous tuning of a spin qubit](https://www.nature.com/articles/s41928-025-01562-4) — A hardware-tuning workflow combining learned classifiers, Bayesian optimization, and experimental feedback from an unenergized device through Rabi oscillations.<br>
  **Reproduction:** [data](https://doi.org/10.5281/zenodo.17745219) · [code](https://github.com/oxquantum-repo/fully-autonomous-tuning) · **hardware:** compatible double-quantum-dot experiment · a dummy pipeline runs locally; full tuning requires live transport measurements and control integration. `[2026] [hardware] [open-code] [public-data]`

- [Using detector likelihood for benchmarking quantum error correction](https://doi.org/10.1103/PhysRevA.111.052452) — Calibrates a simple effective-uniform simulation from measured detector likelihood, bridging complex hardware behavior and reproducible logical-error studies.<br>
  **Reproduction:** [data and code](https://github.com/hetenyib/detector_likelihood_benchmarking) · **hardware:** IBM Floquet- and 3-CX-code memory experiments · **simulation:** matched effective-uniform models with released simulated traces and notebooks. `[2025] [hardware] [simulation] [open-code] [public-data]`

#### 🌪️ Hardware-informed noise simulation and data generation

- [Scalable Noise Characterization of Syndrome-Extraction Circuits with Averaged Circuit Eigenvalue Sampling](https://doi.org/10.1103/PRXQuantum.6.010334) — ACES designs syndrome-extraction experiments that estimate Pauli gate-error probabilities and layer-averaged spatial correlations; the complete characterization procedure is demonstrated in circuit-level simulation of a distance-25 surface code with more than 1,000 qubits.<br>
  **Reproduction:** [code](https://github.com/evanhockings/QuantumACES.jl/tree/scalable_aces) · **simulation:** Stim-backed ACES characterization for surface-code syndrome-extraction circuits, with decoder-prior evaluation and a Qiskit export path for device execution. `[2025] [simulation] [open-code]`

- [Characterising the failure mechanisms of error-corrected quantum logic gates](https://www.nature.com/articles/s41467-026-71773-6) — Device-fit simulation of memory and lattice-surgery stability experiments identifies mid-circuit measurement and idling as key failure mechanisms on IBM’s heavy-hex hardware.<br>
  **Reproduction:** [data and evaluation code](https://doi.org/10.5281/zenodo.18993470) · **hardware:** distance-3 heavy-hex memory and stability experiments on IBM’s 156-qubit Heron r2 Marrakesh processor · **simulation:** Stim model fit to 1Q/2Q depolarizing, measurement, reset, and idle errors, followed by parameter sweeps. `[2026] [hardware] [simulation] [open-code] [public-data]`

- [Simulation of thermal-relaxation noise for quantum error correction](https://doi.org/10.1103/hgnj-v4j7) — Composite amplitude-damping and dephasing decompositions enable stabilizer-compatible thermal-relaxation simulation beyond Pauli twirling, including an exact positive Clifford-and-reset regime when T₂ ≤ T₁.<br>
  **Reproduction:** [public artifact](https://github.com/seangarn32/Composite-Decomposition) · **simulation:** superconducting T₁/T₂ thermal relaxation in surface- and bivariate-bicycle-code memory experiments; the artifact includes simulation files, experiment data, and figure generators. `[2026] [simulation] [public-artifact]`

- [FTPrimitiveBench: A Benchmark Suite for Logical Computation Under Hardware-Motivated and Biased Noise Models](https://arxiv.org/abs/2605.04049) — A benchmark substrate for logical computation, exposing interactions among structured noise, fault-tolerant primitive, and decoder rather than limiting evaluation to memory experiments.<br>
  **Reproduction:** [code](https://github.com/ShuwenKan/FTPrimitiveBench) · **simulation:** [Stim](https://github.com/quantumlib/Stim) circuits with detector/observable annotations for memory, lattice surgery, transversal H, and lattice-surgery S · Pauli/measurement bias, calibration-derived profiles, and spatial or spatiotemporal non-uniformity. `[2026] [preprint] [simulation] [benchmark] [open-code]`

#### 🎮 Simulation-native QEC system search

- [Simultaneous discovery of quantum error correction codes and encoders with a noise-aware reinforcement learning agent](https://www.nature.com/articles/s41534-024-00920-y) — A noise-aware PPO agent co-discovers stabilizer codes and encoding circuits under specified Pauli-noise, gate-set, and connectivity constraints.<br>
  **Reproduction:** [code and notebooks](https://github.com/jolle-ag/qdx) · **simulation:** vectorized JAX Clifford simulation with a Knill–Laflamme reward · fixed symmetric-depolarizing `[[7,1,3]]` and biased-noise `[[6,1]]` demos · up to 25 physical qubits and distance 5 in the paper. `[2024] [simulation] [open-code]`

- [Optimizing hypergraph product codes with random walks, simulated annealing and reinforcement learning](https://arxiv.org/abs/2501.09622) — Projective-simulation RL rewires Tanner graphs to optimize HGP codes against erasure-channel logical failure, then tests transfer under BP+OSD bit-flip decoding.<br>
  **Reproduction:** [code](https://github.com/BrunoCAF/ps-hgp-qec) · [released parity-check matrices](https://arxiv.org/abs/2501.09622) · **simulation:** quantum erasure channel with Monte-Carlo ML/GF(2) evaluation · `(3,4)`-LDPC seeds producing `[[625,25]]`, `[[1600,64]]`, and `[[2025,81]]` HGP codes. `[2025] [simulation] [open-code]`


<a id="decoder-systems"></a>

### 🧠 Decoder systems

#### 🧷 Device-conditioned decoding

- [Learning high-accuracy error decoding for quantum processors (AlphaQubit)](https://www.nature.com/articles/s41586-024-08148-8) — A recurrent-transformer decoder using Sycamore syndrome data and soft-readout/leakage information; its distance-3–11 simulations additionally model crosstalk. It beats the reported tensor-network baseline on distance-3 and distance-5 hardware data, while distance-11 remains realistic-noise simulation.<br>
  **Reproduction:** [Pauli+ simulation data and loading docs](https://storage.mtls.cloud.google.com/gdm-qec) · [Sycamore memory data](https://doi.org/10.5281/zenodo.6804040) · **hardware:** distance-3 and distance-5 Sycamore memory experiments · **simulation:** distance-3–11 Pauli+ noise with crosstalk · detailed architecture pseudocode in the supplement; no official training-code release. `[2024] [hardware] [simulation] [public-data]`

- [Optimization of decoder priors for accurate quantum error correction](https://doi.org/10.1103/PhysRevLett.133.150603) — RL-inspired calibration of hardware-informed decoder priors in repetition- and surface-code memory experiments on Google’s Sycamore processor.<br>
  **Reproduction:** **hardware:** repetition- and surface-code memory experiments on Google’s Sycamore processor · a public code or dataset artifact is not yet indexed here. `[2024] [hardware]`

- [A fault-tolerant neutral-atom architecture for universal quantum computation](https://doi.org/10.1038/s41586-025-09848-5) — Cross-platform system evidence using loss-aware ML decoding on a 448-atom neutral-atom processor; the reported decoder remains distance- and circuit-specific.<br>
  **Reproduction:** **simulation:** supplementary material includes the repeated-QEC [Stim](https://github.com/quantumlib/Stim) circuit and published error model · **hardware:** 448-atom neutral-atom processor · supporting data are otherwise available from the authors on request. `[2026] [hardware] [simulation] [data-restricted]`

#### 🧬 Logical workloads and scale-out

- [Learning to decode logical circuits (MCCD)](https://www.nature.com/articles/s43588-025-00897-4) — Modular LSTM decoding for correlated errors in entangling logical circuits.<br>
  **Reproduction:** [data](https://doi.org/10.5281/zenodo.17196063) · [code](https://doi.org/10.5281/zenodo.17196115) · **simulation:** [Stim](https://github.com/quantumlib/Stim) · surface-code circuit-level noise motivated by neutral-atom experiments · mirror-symmetric random logical Clifford circuits at distance 3 and 5. `[2025] [simulation] [open-code] [public-data]`

- [Machine learning message-passing for scalable QLDPC decoding (Astra)](https://www.nature.com/articles/s41534-025-01033-w) — A graph-native learned message-passing decoder for surface and bivariate-bicycle codes with distance extrapolation.<br>
  **Reproduction:** [code](https://github.com/arshpreetmaan/astra) · **simulation:** code-capacity depolarizing noise on Tanner graphs · training at lower and evaluation at larger code distances. `[2025] [simulation] [open-code]`

<a id="controlled-simulation-and-decoder-evaluation"></a>

#### 🥊 Simulation and decoder evaluation

- [decoder-bench: Benchmarking Decoders for Quantum Error Correction](https://doi.org/10.1109/IISWC66894.2025.00032) — A shared-trace benchmark that separates decoder quality from private simulator and workload choices; its registry supplies adapters for several classical decoders and can be extended.<br>
  **Reproduction:** [data](https://doi.org/10.5281/zenodo.16914504) · [code](https://github.com/satvikmaurya/decoder-bench) · **simulation:** [Stim](https://github.com/quantumlib/Stim)-generated HDF5 check matrices, syndromes, and observables for surface, bivariate-bicycle QLDPC, color-code memory, and surface-code lattice surgery under code-capacity, phenomenological, and circuit-level noise. `[2025] [simulation] [benchmark] [open-code] [public-data]`

- [PyMatching](https://github.com/oscarhiggott/PyMatching) — A minimum-weight-perfect-matching decoder baseline. `[open-code] [supporting-tool]`

- [QEC LEGO Bench](https://qec-lego-bench.readthedocs.io/en/latest/) — A latency-aware streaming-decoder benchmark that converts decoding delay into induced idle error; the authors explicitly label the package very early-stage. `[benchmark] [open-code]`

<a id="runtime-and-adaptive-operation"></a>

### ⚡ Runtime and adaptive operation

#### ⏱️ Runtime deployment and its measurement contract

- [Quantum error correction below the surface code threshold](https://www.nature.com/articles/s41586-024-08449-y) — A below-threshold QEC system landmark on Willow. Its high-accuracy neural decoder is offline; the actual real-time path is a Sparse Blossom streaming stack.<br>
  **Reproduction:** [hardware data](https://doi.org/10.5281/zenodo.13273331) · **hardware:** Willow surface-code QEC experiments · benchmark offline decoders against the release · the paper’s real-time Sparse Blossom implementation is not released as a runnable artifact. `[2025] [hardware] [public-data] [latency-reported]`

- [StabilizerBench](https://arxiv.org/abs/2604.21287) — A benchmark for AI-assisted QEC circuit synthesis; useful for evaluation, not a real-time deployment result.<br>
  **Reproduction:** [benchmark implementation](https://github.com/uw-math-ai/quantum-ai) · **simulation:** Stim circuit tasks with automated verification oracles and task-specific metrics. `[2026] [preprint] [benchmark] [open-code]`

#### 🔁 Closed-loop adaptation

- [Reinforcement learning control of quantum error correction](https://www.nature.com/articles/s41586-026-10759-2) — Uses detection events to update more than 1,000 QEC control parameters across repeated Willow experiments under drift.<br>
  **Reproduction:** [experiment data](https://doi.org/10.5281/zenodo.17566521) · **hardware:** repeated Willow QEC runs under drift · **simulation:** proprietary dynamic surface-code models scale the policy study to distance 15 · source code and simulator are not public. `[2026] [hardware] [simulation] [public-data] [code-closed]`

- [Real-time quantum error correction beyond break-even](https://doi.org/10.1038/s41586-023-05782-6) — A historical precursor in which model-free RL optimized bosonic-QEC control beyond break-even.<br>
  **Reproduction:** **hardware:** bosonic-QEC experiment · a public code or dataset artifact is not yet indexed here. `[2023] [hardware] [historical-precursor]`

- [Realizing a deep reinforcement learning agent for real-time quantum feedback](https://www.nature.com/articles/s41467-023-42901-3) — Direct-on-experiment RL training with sub-microsecond FPGA feedback for a superconducting qubit; important for control, but not a full QEC system.<br>
  **Reproduction:** [experiment data](https://doi.org/10.3929/ethz-b-000637125) · **hardware:** superconducting qubit with sub-microsecond FPGA feedback · analysis code is available from the authors on request · live execution requires FPGA-integrated hardware. `[2023] [hardware] [latency-reported] [historical-precursor]`

<a id="radar"></a>

## 📡 Radar — What's new?

The update feed.

### 🔥 Decoder

- [Learning to decode logical circuits (MCCD)](https://www.nature.com/articles/s43588-025-00897-4) — Modular LSTM decoding for correlated errors in entangling logical circuits.<br>
  **Reproduction:** [data](https://doi.org/10.5281/zenodo.17196063) · [code](https://doi.org/10.5281/zenodo.17196115) · **simulation:** [Stim](https://github.com/quantumlib/Stim) · neutral-atom-motivated surface-code circuit-level noise · mirror-symmetric random logical Clifford circuits at distance 3 and 5. → [Decoder systems](#decoder-systems) `[2025] [simulation] [open-code] [public-data]`

- [Machine learning message-passing for scalable QLDPC decoding (Astra)](https://www.nature.com/articles/s41534-025-01033-w) — A graph-neural decoder that learns message passing on Tanner graphs and transfers from lower to larger surface and bivariate-bicycle code distances.<br>
  **Reproduction:** [code](https://github.com/arshpreetmaan/astra) · **simulation:** code-capacity depolarizing noise on surface- and bivariate-bicycle-code Tanner graphs · train/test scripts included. → [Decoder systems](#decoder-systems) `[2025] [simulation] [open-code]`

- [Ising Decoding](https://github.com/NVIDIA/Ising-Decoding) — Open training and deployment recipes for AI QEC predecoders followed by a global decoder.<br>
  **Reproduction:** [repository](https://github.com/NVIDIA/Ising-Decoding) · **simulation:** public training/inference configs for surface and color codes · optimized inference, ONNX/quantization, and CUDA-Q QEC hand-off recipes. → [Reproducibility ecosystem](#reproducibility-ecosystem) `[2026] [open-code] [industry-artifact] [simulation]`

### 🔥 Runtime

- [Reinforcement learning control of quantum error correction](https://www.nature.com/articles/s41586-026-10759-2) — Detection events steer more than 1,000 QEC control parameters on Willow under drift.<br>
  **Reproduction:** [experiment data](https://doi.org/10.5281/zenodo.17566521) · **hardware:** repeated Willow QEC runs under drift · **simulation:** proprietary dynamic surface-code models scale the policy study to distance 15 · source code and simulator are not public. → [Runtime and adaptive operation](#runtime-and-adaptive-operation) `[2026] [hardware] [simulation] [public-data] [code-closed]`

- [Automating quantum computing laboratory experiments with an agent-based AI framework](https://doi.org/10.1016/j.patter.2025.101372) — A knowledge-based agent workflow for planning, executing, and analysing quantum-laboratory experiments, demonstrated on a three-qubit subset of a 16-qubit superconducting processor.<br>
  **Reproduction:** **hardware:** three-qubit experiments on a 16-qubit superconducting processor · the primary paper describes the workflow; a public implementation is not indexed here. → [Runtime and adaptive operation](#runtime-and-adaptive-operation) `[2025] [hardware]`

- [QCalEval](https://arxiv.org/abs/2604.25884) — A VLM benchmark for quantum-calibration plot understanding; useful for calibration-agent evaluation, not evidence of closed-loop QEC control.<br>
  **Reproduction:** [evaluation scripts](https://github.com/NVIDIA/QCalEval) · [benchmark dataset](https://huggingface.co/datasets/nvidia/QCalEval) · zero-shot, in-context-learning, and judge runners across 243 examples, 87 scenario types, and 22 experiment families. → [Reproducibility ecosystem](#reproducibility-ecosystem) `[2026] [preprint] [benchmark] [open-code] [public-data]`

### 🔥 Simulation

- [Reinforcement Learning for Syndrome Extraction](https://arxiv.org/abs/2609.12020) — PPO searches syndrome-extraction CNOT orderings with an importance-sampled logical-error reward, evaluating schedules in a decoder-in-the-loop simulation up to distance 15.<br>
  **Reproduction:** **simulation:** [Stim](https://github.com/quantumlib/Stim)-based circuit-level schedule evaluation with target-noise decoders and Monte-Carlo importance sampling · no public code or data artifact was indexed at curation. → [Hardware — noise, data, and simulation](#hardware--noise-data-and-simulation) `[2026] [preprint] [simulation]`

- [A Sim-to-Real Study of Surface-Code Decoder Benchmarking](https://arxiv.org/abs/2609.04557) — Compares six decoders across a four-rung synthetic-noise ladder and Willow data; operation-type-specific rates are sufficient for decoder-rank agreement with hardware in the reported study.<br>
  **Reproduction:** **hardware:** Willow data at three code distances, two bases, and 15 round counts · **simulation:** increasingly structured circuit-noise ladder with accuracy and latency evaluation · authors state that pipeline and per-shot outcomes are released, but a stable artifact link was not indexed at curation. → [Decoder systems](#decoder-systems) `[2026] [preprint] [hardware] [simulation] [benchmark]`

- [QMCtwin: Master-Equation Simulation of Syndrome Statistics Beyond Pauli Noise](https://arxiv.org/abs/2606.19848) — A 97-qubit surface-code digital twin models relaxation, dephasing, coherent miscalibration, residual ZZ, and detuning to generate decoder-facing syndrome statistics beyond Pauli twirling.<br>
  **Reproduction:** [circuits, data, and figure scripts](https://github.com/USCqserver/DataRepo-Surface-Code-QMC-Sim) · **simulation:** master-equation modelling of distance-7 syndrome extraction · the full QMC solver is not included in the public artifact. → [Hardware — noise, data, and simulation](#hardware--noise-data-and-simulation) `[2026] [preprint] [simulation] [public-data]`

- [Simulating Quantum Error Correction beyond Pauli Stochastic Errors](https://arxiv.org/abs/2603.18457) — Maps sufficiently small Markovian circuit-level non-Pauli errors to a decoder-facing detector-error model, enabling Monte-Carlo logical-error estimation and noise-adapted decoding beyond Pauli twirling.<br>
  **Reproduction:** **simulation:** surface and bivariate-bicycle syndrome extraction plus magic-state cultivation · no official runnable artifact was indexed at curation. → [Hardware — noise, data, and simulation](#hardware--noise-data-and-simulation) `[2026] [preprint] [simulation]`

<a id="reproducibility-ecosystem"></a>

<a id="ecosystem"></a>

## 🧩 Ecosystem — tools and reproduce

### 📦 Data

- [Sycamore QEC data for AlphaQubit](https://doi.org/10.5281/zenodo.6804040) — Hardware syndrome, soft-readout, and leakage data. `[public-data] [hardware]`
- [Willow below-threshold QEC data](https://doi.org/10.5281/zenodo.13273331) — Hardware surface-code QEC data. `[public-data] [hardware]`
- [Willow RL-control QEC data](https://doi.org/10.5281/zenodo.17566521) — Detection-event and control traces for closed-loop QEC experiments. `[public-data] [hardware]`
- [MCCD data](https://doi.org/10.5281/zenodo.17196063) — Logical-circuit decoding data. `[public-data] [simulation]`
- [Spin-qubit tuning data](https://doi.org/10.5281/zenodo.17745219) — Experimental traces and trained models for autonomous spin-qubit tuning. `[public-data] [hardware]`

### 🧰 Simulation toolchain

- [Stim](https://github.com/quantumlib/Stim) — Stabilizer-circuit simulator for syndrome and decoder-data generation. `[open-code] [supporting-tool]`
- [Sinter](https://github.com/quantumlib/Stim/tree/main/glue/sample) — Sampling and statistical-analysis layer distributed with Stim. `[open-code] [supporting-tool]`
- [Deltakit-Stim](https://github.com/Deltakit/deltakit-stim) — An Apache-2.0 Stim extension for leakage, heralded leakage, and adaptive detector-error-model metadata; useful when a conventional Pauli-only DEM is not the relevant simulation contract. `[open-code] [supporting-tool]`
- [CUDA-Q QEC](https://developer.nvidia.com/cuda-q-qec) — GPU-oriented simulation and QEC development stack. `[industry-artifact] [supporting-tool]`
- [LightStim](https://github.com/QuTone/LightStim) — A protocol-evaluation framework with automated DEM construction and unified decoder backends; it is a reproducible simulation toolchain, not a neutral shared decoder leaderboard. `[2026] [preprint] [simulation] [open-code] [supporting-tool]`
- [Syndrilla](https://github.com/UnaryLab/syndrilla) — A PyTorch simulator and training/evaluation harness for multiple decoder families, configurable error sources, and LER/throughput sweeps; it is an on-demand harness rather than a fixed benchmark corpus. `[2025] [simulation] [open-code] [supporting-tool]`

### 🧠 Decoder implementations and benchmarks

- [PyMatching](https://github.com/oscarhiggott/PyMatching) — MWPM decoder baseline. `[open-code] [supporting-tool]`
- [MCCD code](https://doi.org/10.5281/zenodo.17196115) — Reference implementation for logical-circuit decoding. `[open-code]`
- [Astra](https://github.com/arshpreetmaan/astra) — Open learned message-passing decoder implementation. `[open-code]`
- [Ising Decoding](https://github.com/NVIDIA/Ising-Decoding) — AI decoder training, optimization, and deployment recipes. `[open-code] [industry-artifact]`
- [decoder-bench](https://github.com/satvikmaurya/decoder-bench) — Shared synthetic traces and adapters for reproducible decoder comparisons; see the [controlled-evaluation entry](#controlled-simulation-and-decoder-evaluation) for scope. `[benchmark] [open-code] [public-data]`
- [QEC LEGO Bench](https://qec-lego-bench.readthedocs.io/en/latest/) — Early-stage, latency-aware streaming benchmark infrastructure. `[benchmark] [open-code]`
- [StabilizerBench](https://arxiv.org/abs/2604.21287) — Evaluation for AI QEC-circuit synthesis, not decoder comparison. `[benchmark]`

<a id="parallel-tracks"></a>

## 🛤 Parallel tracks

### 🧮 Fault-tolerant resource optimization

- [Quantum circuit discovery for fault-tolerant logical state preparation with reinforcement learning](https://doi.org/10.1103/gqpr-dgz7) — Reinforcement learning for compact, hardware-constrained fault-tolerant logical state-preparation circuits.<br>
  **Reproduction:** [code](https://github.com/remmyzen/rlftqc) · **simulation:** configurable target stabilizers, gate sets, and connectivity for logical-state preparation, verification-circuit synthesis, and integrated fault-tolerant preparation. `[2025] [simulation] [open-code]`

- [Quantum circuit optimization with AlphaTensor-Quantum](https://www.nature.com/articles/s42256-025-01001-1) — Reinforcement learning and tensor decomposition for explicit fault-tolerant T-count optimization.<br>
  **Reproduction:** [source and runnable demo](https://github.com/google-deepmind/alphatensor_quantum) · [released decompositions](https://doi.org/10.5281/zenodo.14679491) · optional [circuit-to-tensor pipeline](https://github.com/tlaakkonen/circuit-to-tensor) · **simulation:** fault-tolerant T-count optimization · the full research source is not itself runnable. `[2025] [simulation] [open-code] [public-data]`

### 🪄 General AI circuit synthesis and transpilation

- [QSeed: Improving quantum circuit synthesis with machine learning](https://doi.org/10.1109/QCE57702.2023.00093) — ML-guided seeds for unitary synthesis.<br>
  **Reproduction:** **simulation:** unitary-synthesis study · a public implementation is not indexed here. `[2023] [simulation]`

- [Quarl: A learning-based quantum circuit optimizer](https://doi.org/10.1145/3649831) — GNN and reinforcement-learning circuit rewriting with a public artifact.<br>
  **Reproduction:** [artifact and reproduction guide](https://doi.org/10.5281/zenodo.10463907) · **simulation:** circuit-rewrite evaluation with the released optimizer. `[2024] [simulation] [public-artifact]`

- [Practical and efficient quantum circuit synthesis and transpiling with reinforcement learning](https://arxiv.org/abs/2405.13196) — Hardware-aware RL transpilation with an implementation path in the Qiskit AI Transpiler.<br>
  **Reproduction:** [Qiskit AI Transpiler](https://github.com/Qiskit/qiskit-ibm-transpiler) · **simulation:** local AI transpiler passes · cloud-based transpilation workflows require IBM Quantum Premium access. `[2024] [preprint] [open-code] [industry-artifact]`

- [QCircuitBench](https://proceedings.neurips.cc/paper_files/paper/2025/hash/3e343c7fa87656d7e88e9a83cb2a5d10-Abstract-Datasets_and_Benchmarks_Track.html) — Executable evaluation for quantum algorithm and circuit design.<br>
  **Reproduction:** [dataset and generation code](https://github.com/EstelYang/QCircuitBench) · **simulation:** executable circuit-design tasks with automatic validation and verification · demo data on GitHub; full data through the project release. `[2025] [benchmark] [public-data] [open-code]`

### 🩹 Quantum error mitigation (QEM)

- [Machine learning for practical quantum error mitigation](https://www.nature.com/articles/s42256-024-00927-2) — ML-QEM demonstrated on IBM hardware with code and data release.<br>
  **Reproduction:** [code, configurations, training/evaluation scripts, and datasets](https://github.com/qiskit-community/ml-qem/tree/research_branch) · [archival release](https://doi.org/10.5281/zenodo.13769804) · **hardware:** IBM quantum-device experiments. `[2024] [hardware] [open-code] [public-data]`

- [Exponentially tighter bounds on limitations of quantum error mitigation](https://www.nature.com/articles/s41567-024-02536-7) — A theoretical counterweight: generic QEM can require prohibitive sampling overhead.<br>
  **Reproduction:** **theory:** analytical result and proof; no empirical training or hardware artifact is required. `[2024] [theory]`

<a id="related-lists"></a>

## 🌍 Related lists

- [Awesome Quantum Machine Learning](https://github.com/artix41/awesome-quantum-ml) — Quantum computers for machine learning; outside this repository’s scope.
- [Awesome Quantum Software](https://github.com/qosf/awesome-quantum-software) — Broad quantum-software catalogue.
- [ML4QTech Collection](https://github.com/ML4QTech/Collection) — Broader ML-for-quantum-science community collection.

<a id="contributing"></a>

## 🫶 Contributing

Contributions are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) and include a primary source, a neutral description, a reproduction line, evidence tags, artifact status, and the exact workload or noise setting.

<a id="license"></a>

## 📜 License

[MIT](LICENSE) © Rong Tao
