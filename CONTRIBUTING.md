# Contributing to Awesome AI for Practical Quantum Computing

Thank you for helping keep this list useful and evidence-led.

## Before opening a pull request

1. Check that the item belongs to **classical AI/ML for quantum hardware or fault-tolerant computing**. QML, generic quantum-software tools, and vendor announcements are out of scope unless explicitly placed in an adjacent section.
2. Find the **primary source**: the peer-reviewed paper, official project repository, official dataset record, or benchmark specification.
3. Select one canonical section. An item may be cross-linked from infrastructure, but should not be duplicated as if it were several research directions.
4. Confirm that the link and artifact status are current.

## Entry format

Aim for a concise, neutral description of 20–40 words; exceed that only when a material caveat is needed. State what the work does, the engineering outcome, and its most important limit.

```md
- [Project or paper](https://primary.example) — Neutral description of the
  contribution, evaluation setting, and material limitation.
  **Reproduction:** [data](https://data.example) · [code](https://code.example) · **hardware:** concise device or evaluation setting.
  `[2026] [hardware] [public-data] [open-code] [latency-reported]`
```

Use only applicable tags. Peer review is an editorial admission criterion for Core, not an inline tag; use `[preprint]` only when the source has not passed peer review. If code, data, or latency status is unknown, omit the tag rather than guessing. Do not infer hardware validation, code availability, or production readiness from an author affiliation.

## Editorial thresholds

### Core

Core entries must have a clear engineering metric and meet both parts of this threshold:

- selective peer review; and
- either meaningful hardware/system validation **or** a runnable public artifact with a defined workload, noise model, and evaluation contract.

Latency, throughput, resource reporting, cross-device generalization, and follow-on system use are valuable additional evidence, but do not substitute for the threshold above.

### Frontier

Frontier entries need a falsifiable next test and should be labeled as such. A new preprint, vendor release, or generic agent demonstration is not enough on its own.

### Excluded or related

Do not submit:

- quantum-for-AI or generic QML papers;
- generic GPU simulators as AI research directions;
- personal course pages, press releases, or vendor marketing;
- unverified benchmark claims without workload and scoring details;
- duplicate entries or bulk-generated lists.

## Pull-request checklist

- [ ] Primary source and project links work.
- [ ] The entry has one canonical section.
- [ ] The description is neutral and includes a material limitation where needed.
- [ ] Evidence tags accurately distinguish hardware, simulation, code, and data.
- [ ] No proprietary or confidential customer/device information is added.
