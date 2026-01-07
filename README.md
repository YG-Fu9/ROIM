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

### Dataset
Due to file size limitations, only representative data from the first two outer-loop iterations of each case 
are included in the GitHub repository. 
The complete dataset covering all iterations is publicly available at Zenodo: https://doi.org/10.5281/zenodo.18168025.

After downloading, extract the dataset and place it under: rootDir/ROIM/

---


### Data Format (per loop)
Each case folder contains loop-wise text files:
- `alpha_full_<loop>.txt` : friction coefficient used for **alpha → u,v,w,p** prediction in heat-transfer cases
- `ks_full_<loop>.txt`    : thermal conductivity used for **k → T** prediction in heat-transfer cases
- `uvwpT_full_<loop>.txt`  : physical fields (coordinates + velocity/pressure/temperature)

ROIM automatically detects the maximum loop index by scanning:
- `alpha_full_*.txt`

---

## Requirements

- MATLAB (tested with Matlab R2023b)
- No additional toolboxes are strictly required for the core workflow (SVD-based WPOD + linear algebra).

---

## Quick Start

### 1) Prepare data
Place the downloaded case data under `root/ROIM/` as follows:
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
```

---

## Citation

If you use this code or build upon it in your research, please cite:

Fu, YG, et al.  
**Reduced-Order Initialization Model for Accelerating Topology Optimization in Thermal-Fluid System**.  
*Journal / Conference*, Year.
