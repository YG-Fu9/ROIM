# ROIM: Reduced-Order Initialization Model for Accelerating Topology Optimization in Thermal-Fluid Systems

This repository provides a MATLAB implementation of **ROIM (Reduced-Order Initialization Model)**, a reduced-order prediction framework designed to **accelerate repeated numerical simulations in topology optimization (TO)** for thermal–fluid systems.  
ROIM learns latent-space relationships between **previous and current TO iterations** and predicts **high-quality initial fields**, which improves solver convergence and reduces the overall TO runtime.

The core prediction pipeline combines **Weighted Proper Orthogonal Decomposition (WPOD)** with a **reduced-order mapping**:
- WPOD extracts weighted dominant modes from recent iterations,
- a reduced-order mapping predicts modal coefficients for the current iteration,
- reconstructed fields are used as solver initial conditions.

## Highlights

- **Runtime reduction** across four representative TO cases:
  - 2D heat transfer optimization: **22.55%**
  - 2D multi-inlet flow optimization: **35.28%**
  - 3D flow optimization: **33.68%**
  - 3D heat transfer optimization: **32.56%**
- **Prediction accuracy**: mean error as low as **2.09%** in 2D heat transfer optimization.
- **Robustness**: stable performance under boundary-condition fluctuations.
- **Scalability**: in 3D comparative studies, runtime reductions increase from **28.89%** to **54.32%** as model fidelity increases.

> Paper title: **Reduced-Order Initialization Model for Accelerating Topology Optimization in Thermal-Fluid System**  
> (Manuscript under submitted — update this line if needed.)

---

## Repository Structure

### Data Format (per loop)
Each case folder contains loop-wise text files:
- `alpha_full_<loop>.txt` : design field (e.g., SIMP density / penalization-related variable)
- `uvpT_full_<loop>.txt`  : physical fields (coordinates + velocity/pressure/temperature)
- `ks_full_<loop>.txt`    : (optional) thermal conductivity field used for **k → T** prediction in heat-transfer cases

ROIM automatically detects the maximum loop index by scanning:
- `alpha_full_*.txt`

---

## Requirements

- MATLAB (tested with `<your MATLAB version>`)
- No additional toolboxes are strictly required for the core workflow (SVD-based POD + linear algebra).

---

## Quick Start

### 1) Prepare data
Place your case data under:
- `ROIM/Data/2D_heat/`
- `ROIM/Data/2D_multiinlet_flow/`
- `ROIM/Data/3D_flow/`
- `ROIM/Data/3D_heat/`

### 2) Run one case (recommended)
From MATLAB:

```matlab
cd ROIM/src
run_roim_case('2D_heat')

run_roim_case('2D_multiinlet_flow')
run_roim_case('3D_flow')
run_roim_case('3D_heat')

Yuguo Fu, et al.
Reduced-Order Initialization Model for Accelerating Topology Optimization in Thermal-Fluid System.
