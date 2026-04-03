# RouteOpt: Optimization and Learning-Based Shortest Path Analysis

RouteOpt is a notebook-based project that studies the shortest path problem on a weighted grid graph using a hybrid approach that combines:

- **Dijkstra’s Algorithm** for the exact shortest path baseline
- **ADMM (Alternating Direction Method of Multipliers)** for optimization-based routing
- **Graph Neural Networks (GNNs)** for learning path structure from graph data
- **Generative AI analysis** for automated interpretation of routing results

The main notebook in this project is:

- `NOP_RouteOpt.ipynb`

---

## Project Overview

This project explores how classical graph algorithms, numerical optimization, and machine learning can all be applied to the same routing problem.

The workflow is:

1. Build a weighted grid graph
2. Compute the exact shortest path using Dijkstra’s algorithm
3. Reformulate the problem as a constrained flow optimization task
4. Solve the relaxed problem using ADMM
5. Reconstruct a valid route from the optimized flow
6. Train a GNN to learn node/path importance from graph structure
7. Compare all approaches using cost and convergence metrics
8. Use GenAI to generate professional route and performance explanations

---

## Methods Used

### 1. Dijkstra’s Algorithm
Dijkstra’s algorithm is used as the exact benchmark because all edge weights are non-negative. It provides:

- the true shortest path
- the minimum path cost
- a reference for evaluating ADMM and GNN outputs

### 2. ADMM-Based Optimization
The shortest path problem is reformulated as a constrained flow optimization problem:

- Decision variable: edge flow values
- Objective: minimize total routing cost
- Constraints: flow conservation between source and target
- Relaxation: continuous edge-selection values in `[0, 1]`

ADMM is then used to iteratively solve this relaxed optimization problem through:

- **x-update**
- **z-update**
- **u-update**

The notebook also tracks:

- objective convergence
- feasibility residual
- primal residual
- dual residual

### 3. Graph Neural Network (GNN)
A Graph Convolutional Network (GCN)-based model is trained on the graph representation to identify path nodes. The GNN learns from node-level labels derived from the Dijkstra shortest path and predicts a likely route from source to target.

### 4. Generative AI-Based Interpretation
The notebook includes a GenAI component that generates:

- route quality explanations
- evaluation summaries
- professional interpretation of algorithm outputs

This helps make the project more presentation-friendly and easier to explain in demos or academic settings.

---

## Features

- Weighted grid graph generation
- Exact shortest path using Dijkstra
- ADMM-based shortest path optimization
- Path extraction from optimized flow
- GNN-based path learning and prediction
- Convergence plots and residual analysis
- Baseline comparison table
- AI-generated result interpretation

---

## Tech Stack

- **Python**
- **NumPy**
- **Matplotlib**
- **PyTorch**
- **PyTorch Geometric**
- **Pandas**
- **Jupyter Notebook**
- **Google Generative AI API**

---

## File Structure

```text
Numerical_Optimisation_Assignment/
│
├── NOP_RouteOpt.ipynb     # Main notebook containing the full implementation
└── README.md              # Project documentation
```

---

## How It Works

### Graph Construction
A weighted grid graph is created where each node is connected to its neighbors and each edge is assigned a random travel cost.

### Baseline Routing
Dijkstra’s algorithm computes the shortest path from the source node to the target node.

### Optimization Formulation
The graph is converted into an incidence-matrix representation. The shortest path problem is treated as a constrained optimization problem over edge flows.

### ADMM Solver
ADMM iteratively optimizes the routing objective while enforcing flow conservation constraints. Once the solver converges, the final route is reconstructed from the resulting edge flow values.

### GNN Prediction
The graph is converted into PyTorch Geometric format, and a GNN is trained using path-node labels. The trained model predicts a route, which is then compared with the Dijkstra baseline and ADMM solution.

### Evaluation
The notebook compares all methods using:

- path cost
- cost gap from baseline
- convergence behavior
- residual trends

---

## Example Results

From the current notebook run:

- **Dijkstra cost:** `68.5511`
- **ADMM extracted cost:** `68.5511`
- **Absolute cost gap:** `0.000000`
- **GNN cost:** `68.5511`

This shows that, for the tested graph instance, both ADMM and the GNN-based approach matched the Dijkstra shortest path cost.

---

## Installation

Install the required packages before running the notebook:

```bash
pip install numpy matplotlib pandas torch torch-geometric google-generativeai
```

If you are using Jupyter:

```bash
pip install notebook
```

---

## How to Run

1. Clone or download this repository
2. Open `NOP_RouteOpt.ipynb` in Jupyter Notebook or JupyterLab
3. Run the cells in order
4. View:
   - shortest path outputs
   - convergence plots
   - comparison tables
   - GNN predictions
   - GenAI-based summaries

---

## Use Cases

This project is useful for:

- understanding shortest path optimization
- comparing exact, optimization-based, and learning-based methods
- numerical optimization coursework
- graph machine learning demonstrations
- academic presentations and hackathons

---

## Important Note

The uploaded notebook currently contains a **hardcoded Google Generative AI API key**. For safety, you should:

1. remove the key from the notebook
2. regenerate the key if it was ever shared publicly
3. load secrets using environment variables instead

A safer pattern is:

```python
import os
import google.generativeai as genai

genai.configure(api_key=os.getenv("GEMINI_API_KEY"))
```

Then set the key in your environment instead of writing it directly in the notebook.

---

## Future Improvements

- Support larger and more realistic graphs
- Extend from grid graphs to road-network datasets
- Improve GNN training with richer edge/node features
- Add Bellman-Ford and A* for broader baseline comparison
- Build a Streamlit or React dashboard for interactive visualization
- Add robustness tests across multiple random graph instances

---

## Author

**Khushi**

If this repository is part of an academic or portfolio project, you can add your full name, university, and GitHub profile here.

---

## License

You can add a license depending on how you want to share the project, for example:

- MIT License
- Apache 2.0
- No license yet

