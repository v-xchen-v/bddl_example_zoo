# bddl_example_zoo

**BDDL**, originally developed for the BEHAVIOR benchmark and iGibson/iGibson2, is a language for specifying high-level symbolic goals in a concise and structured way. This repository provides hands-on examples for understanding and using the **BDDL (Behavior-Driven Development Language)** in task evaluation, simulation, and robotics research.

This example zoo helps you get started with:
- Writing your own `.bddl` goal specification files.
- Parsing and evaluating symbolic task goals using the `bddl` Python library.
- Integrating BDDL-based goals into your own simulator or learning environment (e.g., IsaacLab, custom robotics frameworks).
- Modify and reuse BDDL as a **problem configuration language** for robotics and simulation

> In particular, this project **breaks down the BDDL-related components of [`genie_sim`](https://github.com/agibottech/genie_sim)** and **simplifies** them to make the logic easier to read, understand, and modify. This serves as an educational and adaptable starting point for using BDDL in your own environments or research pipelines.

---

## 🔧 Installation

Make sure you have Python 3.8+ and install the `bddl` library:

```bash
pip install bddl
```

⚠️ Note: BDDL may attempt to download dataset metadata the first time it runs. This project focuses only on symbolic parsing — no simulation assets are required.

---

## 📁 Project Structure
```
bddl_example_zoo/
├── tasks/ # Contains BDDL files and object scope definitions
│ ├── apple_in_bowl.bddl # Simple BDDL task definition
│ ├── kitchen_clean.bddl # Another task example
│ ├── objects.json # Object scope used in all BDDL tasks
│
├── src/
│ ├── task_evaluator.py # Minimal evaluator for symbolic predicates (IN, ON, etc.)
│ └── predicate_utils.py # Simplified predicate logic adapted from genie_sim
│
├── genie_adapter/ # Genie-sim BDDL logic (simplified or copied for learning)
│ ├── init.py
│ ├── genie_predicates.py # Core predicate checking logic from genie_sim
│ ├── genie_activity_instance.py # Wrapper for BDDL ActivityInstance
│ ├── genie_object_scope.py # Object scope loading logic (optional)
│ └── genie_constants.py # Definitions of known object categories, types, etc.
│
├── main.py # Entry point: parse and evaluate BDDL tasks
├── requirements.txt
└── README.md

```
### 📝 Notes
- `tasks/` contains symbolic task configurations you can edit or extend.
- `src/` has your own simplified predicate evaluator.
- `genie_adapter/` mimics BDDL processing in `genie_sim` to help you understand and reuse its design — **simplified and decoupled from heavy dependencies**.
- `main.py` shows how to parse and test a symbolic goal locally, without a simulator.

---

This structure gives you:
- A working playground for writing your own BDDL task specs
- A simplified mirror of `genie_sim`’s predicate logic
- A foundation for building integration with a simulator like IsaacLab


## 🚀 Quick Start

### 1. Define a BDDL Goal

Inside tasks/apple_in_bowl.bddl:

```bddl
IN(Apple, Bowl) AND On(Bowl, Table)
```

Define the object scope in objects.json:

```json
{
  "objects": ["Apple", "Bowl", "Table"]
}
```

### 2. Run the Example
```bash
python main.py
```
You’ll see output like:
```nginx
Parsed goal conditions:
- ('in', 'apple', 'bowl')
- ('on', 'bowl', 'table')
```
These can then be evaluated in your environment.

## 🔍 Real-World Example: [`genie_sim`](https://github.com/agibottech/genie_sim)

The [`genie_sim`](https://github.com/agibottech/genie_sim) project, developed by AgibotTech, uses BDDL as the **core task specification and evaluation language** to define and benchmark a diverse set of household manipulation tasks across various simulated environments.

In `genie_sim`, BDDL is used to:
- Define the **goal of a task** (e.g., `IN(Apple, Bowl)`)
- Evaluate task success **based on symbolic predicates** during or after simulation
- Support **multi-task generalization and large-scale benchmarking**

You can check out the original usage under:

```bash
genie_sim/genie_sim/tasks/definitions/*.bddl
```

## 🧩 How to Use BDDL as Evaluation Config

1. Write symbolic tasks in .bddl files.

2. Load and parse them using bddl.ActivityInstance.

3. Create mapping logic that translates each symbolic predicate (e.g., IN, ON, CLOSED, etc.) to low-level checks in your simulator.

4. Use that to drive reward shaping, curriculum learning, or task success evaluation.


## 🛠️ Extend This Project
You can modify or extend:

- task_evaluator.py — Add support for new predicates.

- main.py — Connect with your simulator.

- objects.json — Customize object set per task.

## 📚 References
- [BEHAVIOR Benchmark](https://behavior.stanford.edu/)

- [iGibson Simulation Environment](https://github.com/StanfordVL/iGibson)

- [BDDL GitHub](https://github.com/StanfordVL/bddl)

- [Genie-Sim (AgibotTech)](https://github.com/agibottech/genie_sim)

## 🤝 Contributing
Feel free to open issues or submit PRs to contribute new task examples or predicate mappings.

## 📄 License
MIT License
```
Let me know if you'd like to add IsaacLab integration steps or visualization examples next.
```