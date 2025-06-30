# Metaheuristic Optimization Algorithms for PV Panel Model Parameter Estimation

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/FurkanAI/Photovoltaic-Panel-Parameters-Estimation-with-MBBPSO_SA/blob/master/PV_Model_Parameter_Estimation_and_Result.ipynb)

> Click the badge above to launch the notebook directly in Google Colab — no installation required.


This project features various metaheuristic optimization algorithms developed to estimate the parameters of single diode (SDM), double diode (DDM), and triple diode (TDM) models of photovoltaic (PV) panels. The performance of the newly developed algorithms, alongside existing popular metaheuristic algorithms, has been investigated and compared using real-world data.

---

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
  - [Adjustable Algorithm Parameters](#adjustable-algorithm-parameters)
  - [PV Model and Optimization Configuration](#pv-model-and-optimization-configuration)
- [Supported Libraries and Versions](#supported-libraries-and-versions)
- [Contributing](#contributing)
- [License](#License)

---

## Introduction

Accurately modeling the electrical behavior of photovoltaic (PV) panels is crucial for the design, analysis, and optimization of PV systems. The objective of this project is to precisely estimate the fundamental parameters of PV panel models (SDM, DDM, TDM)—such as photocurrent, series resistance, shunt resistance, diode ideality factors, and saturation currents—from experimental V-I (voltage-current) data. This estimation problem is a complex, non-linear optimization challenge, and metaheuristic algorithms prove to be effective tools for its solution.

In this repository, both newly developed metaheuristic algorithms and widely used algorithms from the literature have been implemented and applied to the PV model parameter estimation problem. The code, developed in a Jupyter Notebook environment, is structured to be easily runnable and customizable.

---

## Features

-   **Multiple PV Diode Model Support:** Parameter estimation for the **Single Diode Model (SDM)**, **Double Diode Model (DDM)**, and **Triple Diode Model (TDM)**.
-   **Diverse Metaheuristic Algorithms:** The project includes both newly developed algorithms and popular ones such as Particle Swarm Optimization (**PSO**), Differential Evolution (**DE**), and Simulated Annealing (**SA**).
-   **Adjustable Parameters:** Numerous parameters controlling the algorithms' behavior and the PV modeling process are easily configurable.
-   **Data Input and Output:** Users can input their own measurement data and, optionally, save the results in CSV format.
-   **Reproducible Results:** Option to set a seed for ensuring the repeatability of experiments.

---

## Installation

To run this project, follow these steps:

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/FurkanAI/Photovoltaic-Panel-Parameters-Estimation-with-MBBPSO_SA.git
    cd Photovoltaic-Panel-Parameters-Estimation-with-MBBPSO_SA
    ```
2.  **Ensure Python Version:**
    This project is developed and tested with **Python 3.13.3**. For optimal compatibility, it's recommended to use this version or a newer stable release. You can check your Python version by running `python --version` or `python3 --version` in your terminal.
3.  **Install Required Libraries:**
    It's highly recommended to create a virtual environment before installing dependencies to avoid conflicts with other Python projects.
    ```bash
    # Create a virtual environment
    python3 -m venv venv
    # Activate the virtual environment
    # On Windows:
    # .\venv\Scripts\activate
    # On macOS/Linux:
    # source venv/bin/activate

    # Install the required libraries
    pip install numpy pandas scipy matplotlib ipykernel
    ```
    Alternatively, if you run the Jupyter Notebook, the first cell is designed to automatically install these packages.

---

## Usage

The project is organized as a Jupyter Notebook file. To launch Jupyter Notebook and run the code, follow these steps:

1.  **Launch Jupyter Notebook:**
    From your terminal, navigate to the root directory of the project and run the command:
    ```bash
    jupyter notebook
    ```
2.  **Open the Notebook:**
    In the web interface that opens, locate and click on your project file (e.g., `PV_Model_Parameter_Estimation_and_Result.ipynb`).
3.  **Run the Code:**
    You can run the code by executing the cells sequentially within the notebook or by selecting the "Run All" option.

### Adjustable Algorithm Parameters

At the beginning of the code, there's a set of adjustable parameters that control the behavior of the optimization algorithms and the PV modeling process. You can modify these parameters directly within the Jupyter Notebook file.

```python
# ==============================================================================
#           ADJUSTABLE ALGORITHM PARAMETERS
# ==============================================================================
# This section defines key parameters that control the behavior of various
# optimization algorithms. You can modify these values to influence the
# algorithms' performance and search strategies.
# ==============================================================================

# repetitions: The number of times each algorithm will be run on a given problem.
#              This ensures statistically more reliable results (used for averaging).
repetitions = 1

# seed_generator_seed: Main seed for generating repetitions' unique seeds.
# This value acts as the master seed for the random number generator that produces
# individual seeds for each repetition.
#
# - If a fixed integer value (e.g., 73) is provided:
#   The same sequence of individual repetition seeds will be generated every time
#   the code runs. This ensures that if you run the experiment multiple times,
#   each repetition will start with the exact same initial "randomness",
#   making your results reproducible across runs.
#
# - If set to None:
#   The master seed will be truly random (e.g., based on system time).
#   Consequently, the individual seeds generated for each repetition will be
#   different every time you run the code. This leads to varying results
#   across different executions, as each run will explore different random paths.
seed_generator_seed = None

# General Optimization Parameters
# ------------------------------------------------------------------------------
# iter: The maximum number of iterations for each algorithm run.
#       This determines how long the optimization process will last.
iter = 500

# Swarm-Based Optimization (PSO, BBPSO, MBBPSO, PSO_SA, Dynamic PSO)
# and Differential Evolution (DE) Parameters
# ------------------------------------------------------------------------------
# nop: "Number of Particles" or "Population Size."
#      Defines the number of individuals/particles working simultaneously in the
#      search space for swarm/population-based algorithms. Higher values often
#      offer better solution potential but increase computational cost.
nop = 30

# Simulated Annealing (SA) and PSO-Simulated Annealing (PSO_SA) Parameters
# ------------------------------------------------------------------------------
# T: Initial temperature. Controls the algorithm's probability of accepting
#    worse solutions at the beginning. A higher initial temperature encourages
#    broader exploration of the search space.
T = 5

# alpha: Cooling rate. Determines how much the temperature decreases in each iteration.
#        Typically ranges between 0.85 and 0.99. A lower alpha means faster
#        cooling and potentially earlier convergence.
alpha = 0.97

# Differential Evolution (DE) Algorithm Parameters
# ------------------------------------------------------------------------------
# F: Differential weight factor (Scaling Factor). Controls how much the vector
#    difference is scaled when creating new individuals. Usually between 0.5 and 1.0.
F = 0.5

# CR: Crossover Rate. Determines how often an individual inherits genes (parameters)
#     from its parents. A value between 0 and 1. A higher CR leads to more variation.
CR = 0.2

# Dynamic PSO Parameters
# ------------------------------------------------------------------------------
# w_start: Starting value for the inertia weight (w).
#          Controls how much particles focus on global search. Higher values
#          emphasize exploration.
w_start = 0.9

# w_end: Ending value for the inertia weight (w).
#        As the algorithm progresses, the weight gradually decreases from w_start to w_end.
#        Lower values emphasize local search (exploitation).
w_end = 0.4

# Common Particle Swarm Optimization Parameters (for PSO_SA, PSO, Dynamic PSO)
# ------------------------------------------------------------------------------
# w: Inertia Weight. Determines the influence of a particle's current velocity
#    on its next velocity. A higher 'w' promotes exploration, while a lower 'w'
#    facilitates exploitation/convergence.
w = 0.5

# c1: Cognitive Coefficient or Individual Learning Factor.
#     Controls how much a particle is attracted to its own best-found position.
#     Higher values enhance individual search capability.
c1 = 1.5

# c2: Social Coefficient or Global Learning Factor.
#     Controls how much a particle is attracted to the swarm's overall best-found position.
#     Higher values increase cooperation within the swarm and promote global convergence.
c2 = 1.5


# ==============================================================================
#           PV MODEL AND OPTIMIZATION CONFIGURATION
# ==============================================================================
# This section contains the core parameters for setting up your PV panel
# modeling and optimization process. These values define the specific diode
# model to be used, panel characteristics, data input, and optimization bounds.
# ==============================================================================


# Record Path (Optional)
# If results or process information are to be saved to a file, assign the file path here.
# The path MUST include a '.csv' extension (e.g., 'my_results.csv').
# IMPORTANT: If 'None' (as set), NO recording will be performed. The results will NOT be saved to any file.
# If a string path is provided (e.g., 'my_results.csv'), the results will be saved to that specific file.
record_path = None

# Diode Model Type Selection
# Users select the diode model for PV panel characterization here.
# 1 => Single Diode Model (SDM): A common and simpler model.
# 2 => Double Diode Model (DDM): Includes a second diode for improved accuracy.
# 3 => Triple Diode Model (TDM): Used for situations requiring very high accuracy.
# If an invalid number or any other input is provided, the Single Diode Model (SDM) will be used by default.
diode_model_type = 2

# Panel Characteristics
# Ns: Number of series-connected cells in the panel. Directly influences voltage characteristics.
Ns = 36

# Vth: Thermal voltage at 25°C. A key parameter in the diode's current-voltage relationship.
# It's calculated as: Vth = (k * T) / q
# where:
# k = Boltzmann's constant (1.380649 × 10^-23 J/K)
# T = Absolute temperature in Kelvin (e.g., 25°C = 298.15 K)
# q = Elementary charge (electron charge) (1.602176634 × 10^-19 C)
Vth = 0.02585

# Measured Data
# measured_voltage_array: NumPy array containing measured voltage values from the PV panel.
# measured_current_array: NumPy array containing measured current values from the PV panel.
# Users can input their own measurement data here to calculate panel parameters
# (e.g., Iph, Rs, Rsh, etc.) based on the selected diode model.
measured_voltage_array = None
measured_current_array = None

# Model Parameter Bounds
# parameters_bounds: A NumPy array defining the lower and upper limits for each diode model parameter.
# These bounds ensure that parameters remain within realistic ranges during the optimization process.
# Parameters and Their Descriptions:
# Iph (Photocurrent): Current generated due to solar irradiance.
# Rs (Series Resistance): Resistance from internal series connections within the panel.
# Rsh (Shunt Resistance): Parallel resistance representing leakage currents within the panel.
# n1, n2, n3 (Diode Ideality Factors): Indicate deviation of diodes from ideal behavior.
# Io1, Io2, Io3 (Saturation Currents): Reverse saturation currents of the diodes.
parameters_bounds = np.array([
# Low Limit | High Limit
    [4.5,           5.5],          # Iph (Photocurrent)
    [0.0,           0.5],          # Rs (Series Resistance)
    [1e-9,        500.0],          # Rsh (Shunt Resistance)
    [1.0,           2.0],          # n1 (1st Diode Ideality Factor)
    [1e-9,        10e-6],          # Io1 (1st Diode Saturation Current)
    [1.2,           2.0],          # n2 (2nd Diode Ideality Factor - Only for DDM and TDM)
    [1e-9,        10e-6],          # Io2 (2nd Diode Saturation Current - Only for DDM and TDM)
    [1.4,           2.0],          # n3 (3rd Diyot Ideality Factor - Only for TDM)
    [1e-9,        10e-6]           # Io3 (3rd Diode Saturation Current - Only for TDM)
])
```
---

## Supported Libraries and Versions

This project is developed and tested with **Python 3.13.3**. For optimal compatibility, it's recommended to use this version or a newer stable release.

This project utilizes the following Python libraries. For optimal compatibility, it's recommended to use the specified versions or newer:

-   `math` (Python standard library)
-   `time` (Python standard library)
-   `typing` (Python standard library)
-   `functools` (Python standard library)
-   `datetime` (Python standard library)
-   `warnings` (Python standard library)
-   `ast` (Python standard library)
-   `numpy`: For numerical operations and data processing. Recommended version: **1.24.0 or higher**.
-   `pandas`: For data analysis and manipulation. Recommended version: **1.5.0 or higher**.
-   `scipy`: For scientific computing and optimization algorithms (`scipy.optimize.root_scalar`, `scipy.stats.wilcoxon`). Recommended version: **1.9.0 or higher**.
-   `matplotlib`: For data visualization. Recommended version: **3.6.0 or higher**.

*Note: If you need more specific information about library versions, please feel free to ask.*

---

## Contributing

If you wish to contribute to the development of this project, please do not hesitate to open a [pull request](https://github.com/FurkanAI/Photovoltaic-Panel-Parameters-Estimation-with-MBBPSO_SA/pulls) or create an [issue](https://github.com/FurkanAI/Photovoltaic-Panel-Parameters-Estimation-with-MBBPSO_SA/issues).

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
