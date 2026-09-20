# Phase-Conditioned-FF-Neuron-Routing-for-Agents
Extending GRIFFIN to Agents

# Phase-Conditioned FF-Neuron Routing for LLM-Based Program Repair

> Exploring an extension of GRIFFIN-style input-dependent FF-neuron routing to LLM-based automated program repair.

## Overview

Large language models used as program-repair agents perform different tasks throughout a repair trajectory. A typical repair process can be divided into several phases:

- **Analyze** — understand the issue and inspect the repository
- **Detect** — identify the source of the bug
- **Edit** — modify the relevant code
- **Test** — execute tests and validate the proposed repair

Although these phases correspond to different agent-level objectives, the underlying language model remains the same.

This project investigates whether the model's internal computation also changes systematically between these phases.

The main hypothesis is:

> **Different repair phases may rely on different subsets of FF neurons, and these phase-specific subsets may be exploitable for sparse computation and neuron routing.**

The project takes the input-dependent routing intuition from **GRIFFIN** and studies whether it can be extended to the phase structure of automated program-repair agents.

---

## Research Question

The central question is:

> **Can FF-neuron routing be conditioned on the phase of an LLM-based repair agent?**

For a repair trajectory divided into phases


P = {Analyze,Detect,Edit,Test},


we investigate whether each phase has a characteristic set of active FF neurons:


$E_{A}, E_{D}, E_{E}, E_{T}$


More generally, for a model input $X_{p}$ belonging to phase p,


$X_{p} \rightarrow E_{p}^{FF}$


We then study:

1. **Phase specificity** — Are the selected neuron sets different across phases?
2. **Temporal stability** — Are they stable within a phase?
3. **Reuse** — Can a phase-specific set be selected once and reused?
4. **Efficiency** — Can this routing reduce computation?
5. **Repair quality** — Does sparse routing preserve repair performance?

---

## Motivation

GRIFFIN explores input-dependent FF-neuron selection and routing.

This project asks whether the **agent's current role** can provide another useful conditioning signal.

Instead of considering only:


$X \rightarrow E_{X}$


we consider:


$(X, p) \rightarrow E_{p}$


where p denotes the current repair phase.

The goal is not to assume that phase-specific circuits exist, but to test this hypothesis empirically.

---

## Repair-Agent Phases

The initial phase decomposition is:

| Phase | Main objective |
|---|---|
| Analyze | Understand the issue, repository, and relevant code |
| Detect | Localize and reason about the underlying bug |
| Edit | Modify the source code to address the bug |
| Test | Validate the proposed repair and inspect failures |

A trajectory can therefore be represented as:

```text
Repair Trajectory
       │
       ├── Analyze ──→ E_{A}
       │
       ├── Detect  ──→ E_{D}
       │
       ├── Edit    ──→ E_{E}
       │
       └── Test    ──→ E_{T}
