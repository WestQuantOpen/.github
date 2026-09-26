<div align="center">

# WestQuant Open

### Open infrastructure for AI x Quantum Algorithm Engineering

**Generate ML data from quantum programs. Compare software stacks. Search for better representations.**

</div>

---

<div align="center">

[![PyPI](https://img.shields.io/pypi/v/westquant)](https://pypi.org/project/westquant/)
[![PyPI](https://img.shields.io/pypi/v/westquant-qcsc)](https://pypi.org/project/westquant-qcsc/)
[![License](https://img.shields.io/badge/license-Apache--2.0-blue)](https://www.apache.org/licenses/LICENSE-2.0)
[![Python](https://img.shields.io/badge/python-3.10+-blue)](https://www.python.org/)
[![Discussions](https://img.shields.io/badge/discussions-join%20us-blue)](https://github.com/orgs/WestQuantOpen/discussions)

</div>

---

## What WestQuant Open does

WestQuant Open is an open research infrastructure for generating machine-learning data from quantum programs, comparing quantum software stacks, and searching for better circuit representations and compilation strategies across frameworks and hardware targets.

The unique layer:

```
Quantum program -> representation -> transformation sequence -> hardware mapping -> result
```

### Five things WestQuant can do

1. **Generate ML training data** from quantum algorithms
2. **Search representation/transformation schedules** across frameworks
3. **Compare Qiskit / PennyLane / Cirq** compilation pipelines
4. **Optimize circuits** for different hardware targets
5. **Record complete transformation provenance** for reproducibility

## Quick start

```bash
pip install westquant[qiskit]
```

```python
from westquant import optimize

result = optimize(circuit, framework="qiskit", backend=backend, budget=64)
print(result.pareto_front)
```

### QPU Budget Predictor

Estimate required QPU budget from problem structure — before any quantum execution:

```bash
pip install westquant-qcsc
```

```python
from qcsc import QPUBudgetPredictor, ProblemProfile

profile = ProblemProfile(problem="MaxCut", n_qubits=16, p=3, graph_family="GEO")
predictor = QPUBudgetPredictor()
budget = predictor.estimate(profile)
# 1024 shots, 2070x reduction vs naive, quality=0.9961
```

## Packages

### Core

| Package | Description |
|---------|-------------|
| **[westquant](https://github.com/WestQuantOpen/westquant)** | Umbrella package — representation search |
| **[westquant-core](https://github.com/WestQuantOpen/westquant-core)** | WQIR, RepGraph, plugin contracts |
| **[westquant-qcsc](https://github.com/WestQuantOpen/westquant-qcsc)** | Semantic QPU Minimization + QPU Budget Predictor |

### Framework integrations

| Package | Description |
|---------|-------------|
| **[westquant-qiskit](https://github.com/WestQuantOpen/westquant-qiskit)** | Qiskit transpiler plugins |
| **[westquant-pytket](https://github.com/WestQuantOpen/westquant-pytket)** | pytket compiler pass search |
| **[westquant-pennylane](https://github.com/WestQuantOpen/westquant-pennylane)** | PennyLane transform search |
| **[westquant-pulser](https://github.com/WestQuantOpen/westquant-pulser)** | Pulser neutral-atom search |

### Infrastructure

| Package | Description |
|---------|-------------|
| **[westquant-orchestrator](https://github.com/WestQuantOpen/westquant-orchestrator)** | Cross-framework normalization |
| **[westquant-bridges](https://github.com/WestQuantOpen/westquant-bridges)** | Cirq/Braket/QIR/OpenQASM bridges |

### Research

| Repo | Description |
|------|-------------|
| **[qpu-mini](https://github.com/WestQuantOpen/qpu-mini)** | Paper A — QPU-efficient quantum graph optimization (510-2070x reduction) |
| **[representation-stack](https://github.com/WestQuantOpen/representation-stack)** | Artifact #001 — Representation search for quantum optimization |

## Architecture

```
                    ┌─────────────────────────────────────────┐
                    │          WestQuant Open Layer            │
                    │                                         │
                    │   Quantum program                        │
                    │        │                                │
                    │        ▼                                │
                    │   ┌─────────┐    ┌──────────────┐       │
                    │   │  WQIR   │───▶│  RepGraph    │       │
                    │   │ (IR)    │    │  (search     │       │
                    │   └────┬────┘    │   space)     │       │
                    │        │         └──────┬───────┘       │
                    │        ▼                │              │
                    │   ┌─────────────┐        │              │
                    │   │ Transform   │◀───────┘              │
                    │   │ Registry    │                       │
                    │   └─────┬───────┘                       │
                    │         ▼                               │
                    │   ┌─────────────┐    ┌──────────────┐   │
                    │   │  Verifier   │───▶│  Planner     │   │
                    │   └─────────────┘    └──────────────┘   │
                    │         │                               │
                    │         ▼                               │
                    │   Optimized circuit + ML dataset +       │
                    │   provenance trace + benchmark results  │
                    └─────────────────────────────────────────┘
                         ▲           ▲           ▲
                    ┌────┴────┐ ┌────┴────┐ ┌────┴────┐
                    │ Qiskit  │ │PennyLane │ │  Cirq   │
                    └─────────┘ └─────────┘ └─────────┘
```

See [full architecture](https://github.com/WestQuantOpen/westquant/blob/main/docs/ARCHITECTURE.md).

## Design philosophy

WestQuant asks three questions in order:

1. **Does this operation need to happen?** (Eliminate)
2. **Does it need to be quantum?** (Replace with classical)
3. **Only then: which resource should execute it?** (Schedule)

## Research

### Paper A (submitted)

**Optimize the Optimization: QPU-Efficient Quantum Graph Optimization through HPC-First Experimentation**
Submitted to IEEE Transactions on Quantum Engineering.

Key finding: QPU requirement is a structured, predictable function of problem structure — not a fixed constant. 510-2070x shot reduction with ≤0.4% quality loss.

### Paper B (under review)

Systematic mapping review of QPU minimization and quantum workflow systems. Submitted to ACM Computing Surveys.

### Upcoming: Technical Paper

**WestQuantOpen: Cross-Framework Quantum Program Optimization, Representation Scheduling, and ML Dataset Generation**

Four contributions:
- Cross-framework abstraction (Qiskit, PennyLane, Cirq)
- Transformation provenance (every step recorded)
- ML dataset generation (before/after pairs, actions, metrics)
- Representation-policy search (systematic transformation sequence search)

## Benchmark corpus

10 algorithm families, ~2,000 circuits:

| Family | Sizes |
|--------|-------|
| GHZ | 4-100 qubits |
| QFT | 3-30 |
| Grover | 3-20 |
| Bernstein-Vazirani | 4-50 |
| QPE | 3-20 |
| QAOA MaxCut | multiple graph families |
| VQE ansatze | multiple molecules |
| Trotter simulation | varying steps |
| Quantum arithmetic | adders/multipliers |
| Random Clifford | varying density |

See [benchmarks](https://github.com/WestQuantOpen/westquant/blob/main/benchmarks/).

## Community

- **Discussions:** [Join the conversation](https://github.com/orgs/WestQuantOpen/discussions)
- **Contributing:** See [CONTRIBUTING.md](https://github.com/WestQuantOpen/.github/blob/main/CONTRIBUTING.md)
- **Code of Conduct:** See [CODE_OF_CONDUCT.md](https://github.com/WestQuantOpen/.github/blob/main/CODE_OF_CONDUCT.md)
- **Releases:** Monthly on the last Friday — see [release schedule](https://github.com/WestQuantOpen/.github/blob/main/RELEASE_SCHEDULE.md)
- **Project plan:** See [WQO_PROJECT_PLAN.md](https://github.com/WestQuantOpen/westquant/blob/main/WQO_PROJECT_PLAN.md)

## License

Apache-2.0 (core packages) / MIT (qcsc)

## Author

**David Vesterlund** — Vesterlund Ventures, Industrial Research / WestQuant Open Source Project

- Email: david@vesterlundventures.se
- ORCID: [0009-0000-6455-1141](https://orcid.org/0009-0000-6455-1141)
- Website: [davidvesterlund.com](https://davidvesterlund.com)

<div align="center">

**[Back to top](#westquant-open)**

</div>
