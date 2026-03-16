# CR-solver Documentation

## Description

CR-solver 1.0 (2026)
Written by Dr. Jianing Wang and distributed under the MIT License.

CR-solver is a Python code designed to determine the model parameters of constant-roll inflation in a SR–CR–SR scenario (slow-roll → constant-roll → slow-roll) based on features in the curvature perturbation power spectrum.

This code accompanies the paper:  
"Constant-Roll Inflation: Analytical Formula for Power Spectrum and Implication on Induced Gravitational Wave Spectrum"
Authors: Hayato Motohashi, Shi Pi, Yuichiro Tada, Jianing Wang.
Users of this code are kindly requested to cite this paper.

CR-solver leverages [SIGWfast](https://github.com/Lukas-T-W/SIGWfast) to calculate the induced gravitational wave spectrum.

## Prerequisites

CR-solver requires Python 3 and Jupyter Notebook (or JupyterLab).  
We strongly recommend using a virtual environment together with a package manager such as `conda` to manage dependencies.
CR-solver is compiled for NumPy 1.x and does not currently support NumPy 2.x.  Running it with NumPy ≥ 2 may cause crashes.

To get started, download the latest release as a `.zip` archive.  
After extracting the archive, the required files and directory structure will be properly organized in the main project directory.
You can then proceed with installing the required dependencies and running the solver.

## User guide

Users only need to work with the `main.ipynb` notebook to input the initial parameters — specifically, the ratios of wavenumbers and the amplitudes of the two peaks in the curvature perturbation power spectrum.  

Running the notebook will generate the results, including:
constant-roll parameters, curvature perturbation power spectrum, and induced gravitational wave spectrum

### File Content

| File | Description |
|------|-------------|
| `README.md` | Project description and usage instructions |
| `LICENSE` | MIT License |
| `main.ipynb` | Jupyter Notebook main file for computations and running the solver |
| `functionscr.py` | Contains the characteristic functions for the SR–CR–SR scenario (slow-roll → constant-roll → slow-roll). Detailed derivations can be found in the paper "Constant-Roll Inflation: Analytical Formula for Power Spectrum and Implication on Induced Gravitational Wave Spectrum" by Hayato Motohashi, Shi Pi, Yuichiro Tada, and Jianing Wang |
| `libraries` | Folder containing external functions used to calculate gravitational waves, adapted from [SIGWfast](https://github.com/Lukas-T-W/SIGWfast) |

## Input

After installing all the required packages, the user only needs to input the following quantities:
# --------------- input -> --------------- #

k2k1: Ratio of the second peak wavenumber to the first peak wavenumber  
A2A1: Ratio of the second peak amplitude to the first peak amplitude  
Type: Choose `"exact"` for the exact power spectrum or `"smoothed"` for the smoothed one. Any other value will result in an error.

Ahighest: Highest power spectrum amplitude, either comes from the first peak or the second peak

khighest: Wavenumber (or frequency) of highest point in power spectrum

Important:
k2k1 should be larger than 10^0.7,
A2A1 should be larger than 10^-0.25,
and log10(A2A1) ≤ -0.727 + 2.015 * log10(k2k1),
Otherwise, the output should be interpreted with caution.

Values outside these ranges may lead to unreliable solutions. Please refer to the paper for detailed explanations.

# --------------- <- input --------------- #


## Output

After inputting all the required quantities, the code outputs the following:

Constant-roll inflation model parameters:

beta: Half of the second slow-roll parameter. Should be between -3 and -2; values outside this range are considered unreliable as solutions.  
NCR: Duration of the constant-roll stage. 
Please refer to the paper for detailed explanations.

tau_s: Time of the SR-CR transition
k_star: -1/ tau_s
tau_e: Time of CR-SR transition

AIR: Power spectrum amplitude at IR limit

The scatter data used for plotting the GW spectrum is also output.
