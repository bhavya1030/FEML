# FEML: Physics-Informed Neural Network (PINN) Surrogate for FEA

## Overview

**FEML** is a Python toolkit for building, training, and visualizing a surrogate model that predicts Finite Element Analysis (FEA) nodal displacements for beams under various loads and boundary conditions. This project uses a **Physics-Informed Neural Network (PINN)**, which incorporates physical laws directly into the neural network's training process.

The project automates FEA data generation, verifies outputs, prepares data for machine learning, and visualizes both FEA and PINN predictions.

---

## Table of Contents

- [Project Workflow](#project-workflow)
- [Tech Stack & Libraries](#tech-stack--libraries)
- [Directory Structure](#directory-structure)
- [Installation](#installation)
- [Step-by-Step Usage](#step-by-step-usage)
- [Data Formats](#data-formats)
- [Model Details](#model-details)
- [Visualization](#visualization)
- [Troubleshooting & Tips](#troubleshooting--tips)
- [Contributing](#contributing)
- [License](#license)

---

## Project Workflow

1. **FEA Data Generation**: Use Ansys MAPDL to simulate many beam cases with varying loads and boundary conditions.
2. **Verification**: Check the generated data for consistency and correctness.
3. **Data Preparation**: Prepare FEA mesh and simulation results for PINN training.
4. **Model Training**: Train a PINN to predict nodal displacements from input features.
5. **Visualization**: Visualize both FEA and surrogate model predictions.

---

## Tech Stack & Libraries

- **Python 3.8+**
- **Ansys MAPDL** (`ansys-mapdl-core`): For running FEA simulations (requires a licensed installation).
- **NumPy**: Array and numerical operations.
- **Pandas**: Data manipulation and CSV handling.
- **PyTorch**: Deep learning framework.
- **PyVista**: 3D visualization of meshes and results.
- **PyQt5**: GUI for interactive geometry and load setup (optional, for advanced users).

---

## Directory Structure

```
FEML/
├── Data/
│   └── Simulation_Data/
│       └── Simulation_Output/
├── app/
│   └── main_window.py
├── docks/
├── src/
│   └── postprocess.py
├── viewport/
│   ├── beam_viewport.py
│   └── geometry_factory.py
├── dataGen.py
├── verifyData.py
├── dataPreparation.py
├── visualization.py
├── modelArchitecture.py
├── training.py
├── requirements.txt
└── README.md
```

---

## Installation

### 1. Clone the Repository

```sh
git clone https://github.com/yourusername/FEML.git
cd FEML
```

### 2. Set Up Python Environment

```sh
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install Dependencies

```sh
pip install numpy pandas pyvista torch torchvision torchaudio pyqt5
pip install ansys-mapdl-core
```

> **Note:** Ansys MAPDL must be installed and licensed on your machine to run FEA simulations.

---

## Step-by-Step Usage

### 1. Generate FEA Data

Runs Ansys MAPDL to simulate multiple beam cases and saves results.

```sh
python dataGen.py
```
- Output: Numpy arrays and CSV files in `Data\Simulation_Data\Simulation_Output`.

### 2. Verify Data Consistency

Checks the shapes and integrity of the generated data.

```sh
python verifyData.py
```

### 3. Prepare Data for PINN

Processes FEA mesh and results into a format suitable for PINN training.

```sh
python dataPreparation.py
```

### 4. Train the PINN Model

Trains the surrogate PINN model on the dataset.

```sh
python training.py
```

### 5. Visualize Results

Visualizes FEA and/or model predictions.

```sh
python visualization.py
```

---

## Data Formats

- `fixed_node_coords.npy`: (N_nodes, 3) — Node coordinates (x, y, z).
- `fixed_node_nums.npy`: (N_nodes,) — Original MAPDL node numbers.
- `fixed_connectivity.npy`: Element connectivity.
- `all_displacement_tensors.npy`: (N_cases, N_nodes, 3) — Displacements for each case.
- `simulation_input_metadata.csv`: Metadata for each case (load position, magnitude, etc.).

---

## Model Details

- **Model Type**: Physics-Informed Neural Network (PINN)
- **Input Features**: `[x, y, z, Load_Position_X_m, Load_Magnitude_N]` per node.
- **Output**: `[dx, dy, dz]` — Predicted displacement per node.
- **Default Hyperparameters**:
  - Hidden dimension: 64
  - Layers: 4
  - Batch size: 32

---

## Visualization

- Uses `pyvista` to render undeformed and deformed geometries.
- Shows boundary conditions and applied force arrows.
- Can visualize both FEA and surrogate model predictions.

---

## Troubleshooting & Tips

- **Paths**: Run scripts from the repository root, or update path constants at the top of each script.
- **Large-scale Data**: `dataGen.py` can generate thousands of cases; ensure you have enough compute and storage.
- **MAPDL Errors**: Ensure Ansys MAPDL is installed and licensed.

---

## Contributing

- Fork the repo and create a feature branch.
- Submit pull requests with clear descriptions.
- Follow existing code style and conventions.

---

## License

MIT License (or specify your license here).

---

## Acknowledgements

- Built with [Ansys MAPDL](https://www.ansys.com/products/structures/ansys-mechanical) and [PyTorch](https://pytorch.org/).
