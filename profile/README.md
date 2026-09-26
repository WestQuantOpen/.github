<div align="center">

# WestQuant Open

### Search the representation, not just the parameters.

**Open-source tools for efficient quantum computing — QPU minimization, representation search, and workflow optimization.**

</div>

---

<div align="center">

[![PyPI](https://img.shields.io/pypi/v/westquant)](https://pypi.org/project/westquant/)
[![PyPI](https://img.shields.io/pypi/v/westquant-qcsc)](https://pypi.org/project/westquant-qcsc/)
[![License](https://img.shields.io/badge/license-Apache--2.0-blue)](https://www.apache.org/licenses/LICENSE-2.0)
[![Python](https://img.shields.io/badge/python-3.10+-blue)](https://www.python.org/)
[![Discussions](https://img.shields.io/badge/discussions-join%20us-blue)](https://github.com/orgs/WestQuantOpen/discussions)

</div>

## What we do

Quantum processing units (QPUs) are scarce, expensive, and queued. WestQuant Open builds open-source tools that help quantum practitioners use QPU time more efficiently — and avoid it entirely where classical computation suffices.

Our research shows that the required QPU budget is not a fixed algorithmic constant but a **structured, predictable function** of the problem instance and workflow policy:

```
QPU_requirement = f(graph, problem, n, depth, quality_target, hardware)
```

By separating classical parameter optimization from a single QPU evaluation, we achieve **510–2070× shot reduction** with **≤0.4% quality loss** across graph optimization problems.

## Projects

### Core packages

| Package | PyPI | Description |
|---------|------|-------------|
| **[westquant](https://github.com/WestQuantOpen/westquant)** | [![PyPI](https://img.shields.io/pypi/v/westquant)](https://pypi.org/project/westquant/) | Umbrella package — representation search |
| **[westquant-core](https://github.com/WestQuantOpen/westquant-core)** | [![PyPI](https://img.shields.io/pypi/v/westquant-core)](https://pypi.org/project/westquant-core/) | WQIR, RepGraph, plugin contracts |
| **[westquant-qcsc](https://github.com/WestQuantOpen/westquant-qcsc)** | [![PyPI](https://img.shields.io/pypi/v/westquant-qcsc)](https://pypi.org/project/westquant-qcsc/) | Semantic QPU Minimization optimizer |

### Framework integrations

| Package | PyPI | Description |
|---------|------|-------------|
| **[westquant-qiskit](https://github.com/WestQuantOpen/westquant-qiskit)** | [![PyPI](https://img.shields.io/pypi/v/westquant-qiskit)](https://pypi.org/project/westquant-qiskit/) | Qiskit transpiler plugins |
| **[westquant-pytket](https://github.com/WestQuantOpen/westquant-pytket)** | [![PyPI](https://img.shields.io/pypi/v/westquant-pytket)](https://pypi.org/project/westquant-pytket/) | pytket compiler pass search |
| **[westquant-pennylane](https://github.com/WestQuantOpen/westquant-pennylane)** | [![PyPI](https://img.shields.io/pypi/v/westquant-pennylane)](https://pypi.org/project/westquant-pennylane/) | PennyLane transform search |
| **[westquant-pulser](https://github.com/WestQuantOpen/westquant-pulser)** | [![PyPI](https://img.shields.io/pypi/v/westquant-pulser)](https://pypi.org/project/westquant-pulser/) | Pulser neutral-atom search |

### Infrastructure

| Package | PyPI | Description |
|---------|------|-------------|
| **[westquant-orchestrator](https://github.com/WestQuantOpen/westquant-orchestrator)** | [![PyPI](https://img.shields.io/pypi/v/westquant-orchestrator)](https://pypi.org/project/westquant-orchestrator/) | Cross-framework normalization |
| **[westquant-bridges](https://github.com/WestQuantOpen/westquant-bridges)** | [![PyPI](https://img.shields.io/pypi/v/westquant-bridges)](https://pypi.org/project/westquant-bridges/) | Cirq/Braket/QIR/OpenQASM bridges |

### Research

| Repo | Description |
|------|-------------|
| **[qpu-mini](https://github.com/WestQuantOpen/qpu-mini)** | Paper A — QPU-efficient quantum graph optimization experiments |
| **[representation-stack](https://github.com/WestQuantOpen/representation-stack)** | Artifact #001 — Representation search for quantum optimization |

## Quick start

```bash
pip install westquant[qiskit]
```

```python
from westquant import optimize

result = optimize(circuit, framework="qiskit", backend=backend, budget=64)
print(result.pareto_front)
```

Or use the QPU budget predictor:

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

## Design philosophy

WestQuant asks three questions in order:

1. **Does this operation need to happen?** (Eliminate)
2. **Does it need to be quantum?** (Replace with classical)
3. **Only then: which resource should execute it?** (Schedule)

That ordering is the defining idea of the project.

## Community

- **Discussions:** [Join the conversation](https://github.com/orgs/WestQuantOpen/discussions)
- **Issues:** Report bugs or request features on the relevant repo
- **Contributing:** See [CONTRIBUTING.md](https://github.com/WestQuantOpen/.github/blob/main/CONTRIBUTING.md)
- **Code of Conduct:** We follow the [Contributor Covenant](https://github.com/WestQuantOpen/.github/blob/main/CODE_OF_CONDUCT.md)

## Releases

Monthly releases on the last Friday of each month. See the [release schedule](https://github.com/WestQuantOpen/.github/blob/main/RELEASE_SCHEDULE.md).

## License

Apache-2.0 (core packages) / MIT (qcsc). See individual repos for details.

## Author

**David Vesterlund** — Vesterlund Ventures, Industrial Research / WestQuant Open Source Project

- Email: david@vesterlundventures.se
- ORCID: [0009-0000-6455-1141](https://orcid.org/0009-0000-6455-1141)
- Website: [davidvesterlund.com](https://davidvesterlund.com)

<div align="center">

**[⬆ Back to top](#westquant-open)**

</div>
