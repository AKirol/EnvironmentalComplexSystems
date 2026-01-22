# Random Walk Notebook - User Guide and Theory

## Table of Contents
1. [Introduction](#introduction)
2. [User Guide](#user-guide)
   - [Prerequisites](#prerequisites)
   - [Getting Started](#getting-started)
   - [Running the Notebook](#running-the-notebook)
3. [Theory Behind Random Walks](#theory-behind-random-walks)
   - [One-Dimensional Random Walk](#one-dimensional-random-walk)
   - [Mean-Square Displacement](#mean-square-displacement)
   - [Diffusion and the Diffusion Coefficient](#diffusion-and-the-diffusion-coefficient)
   - [Two-Dimensional Random Walk](#two-dimensional-random-walk)
   - [Central Limit Theorem](#central-limit-theorem)
4. [Examples in the Notebook](#examples-in-the-notebook)
5. [Applications in Environmental Science](#applications-in-environmental-science)
6. [References and Further Reading](#references-and-further-reading)

---

## Introduction

The `random_walk.ipynb` notebook provides an interactive exploration of random walk processes, a fundamental concept in statistical physics, environmental science, and complex systems modeling. Random walks are used to model phenomena ranging from molecular diffusion to animal foraging behavior and pollutant dispersion.

This guide provides both practical instructions for using the notebook and the theoretical foundations underlying random walk processes.

---

## User Guide

### Prerequisites

Before running the notebook, ensure you have the following:

1. **Python 3.7+** installed on your system
2. **Jupyter Notebook or JupyterLab**
3. **Required Python packages:**
   - `numpy` - for numerical computations
   - `plotly` - for interactive visualizations
   - `scipy` - for statistical functions

### Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/AKirol/EnvironmentalComplexSystems.git
   cd EnvironmentalComplexSystems
   ```

2. **Set up a virtual environment (recommended):**
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   pip install -e .
   ```

4. **Launch Jupyter:**
   ```bash
   jupyter notebook notebooks/random_walk.ipynb
   ```
   or
   ```bash
   jupyter lab notebooks/random_walk.ipynb
   ```

### Running the Notebook

The notebook is organized into sequential examples that build understanding progressively:

1. **Execute cells in order** - Each cell builds on previous results
2. **Interactive visualizations** - Plots use Plotly for interactive exploration (zoom, pan, hover)
3. **Modify parameters** - Experiment with different values to see how behavior changes:
   - `mu` - mean step size (drift)
   - `sigma` - standard deviation of steps
   - `num_steps` - number of steps in the walk
   - `num_walkers` - ensemble size for statistical analysis

**Tips:**
- Start by running all cells to see the default behavior
- Then go back and modify parameters in individual examples
- Use `Shift + Enter` to execute a cell and move to the next one
- Use `Ctrl + Enter` to execute a cell without moving

---

## Theory Behind Random Walks

### One-Dimensional Random Walk

A **random walk** is a mathematical model describing a path consisting of a succession of random steps. In one dimension:

- A walker starts at position **x = 0** at time **t = 0**
- At each time step, the walker takes a step of size **Δx**, drawn from a probability distribution
- After **n** steps, the position is: **x(n) = Σᵢ Δxᵢ**

**Key Types:**

1. **Symmetric (Unbiased) Random Walk:**
   - Steps drawn from a distribution with mean μ = 0
   - No preferred direction
   - Equal probability of moving left or right
   - Example: `random_walk(mu=0, sigma=1, num_steps=1000)`

2. **Biased (Asymmetric) Random Walk:**
   - Steps drawn from a distribution with mean μ ≠ 0
   - Preferred direction (drift)
   - Example: `random_walk(mu=0.1, sigma=1, num_steps=1000)` has positive drift

### Mean-Square Displacement

The **mean-square displacement** (MSD) is a fundamental quantity characterizing random walks:

**⟨x²(t)⟩ = 2Dt**

Where:
- **⟨x²(t)⟩** is the mean-square displacement at time t
- **D** is the diffusion coefficient
- **t** is time (proportional to number of steps)

**Key Properties:**
- For symmetric random walks: **⟨x(t)⟩ = 0** (average position returns to origin)
- The **root-mean-square displacement** grows as: **√⟨x²⟩ ∝ √t**
- This is slower than advective motion (∝ t) but faster than logarithmic diffusion

**Physical Interpretation:**
- The MSD measures how far, on average, a particle has moved from its starting position
- Linear growth with time is the signature of **diffusive** behavior
- This relationship is verified in Example 3 of the notebook

### Diffusion and the Diffusion Coefficient

The random walk is intimately connected to **diffusion**, governed by Fick's second law:

**∂C/∂t = D ∇²C**

Where:
- **C(x,t)** is concentration
- **D** is the diffusion coefficient
- **∇²** is the Laplacian operator

**Diffusion Coefficient:**
For a 1D random walk with step size **σ** and time step **τ**:

**D = σ²/(2τ)**

**Key Insights:**
- Random walks provide a microscopic foundation for macroscopic diffusion
- The distribution of walker positions approaches a Gaussian (normal) distribution
- Width of Gaussian: **σₜ = √(2Dt)**

### Two-Dimensional Random Walk

In 2D, the walker moves in a plane with independent steps in x and y directions:

**r²(t) = x²(t) + y²(t)**

**Mean-square displacement in 2D:**

**⟨r²(t)⟩ = 4Dt**

(Factor of 4 instead of 2, accounting for two dimensions)

**Key Properties:**
- 2D walkers are **transient** in dimensions d > 2 (won't return to origin with probability 1)
- 2D walkers are **recurrent** in d ≤ 2 (will eventually return to origin with probability 1)
- Applications: animal foraging, pollutant dispersion in water/air

### Central Limit Theorem

The **Central Limit Theorem (CLT)** explains why walker positions become Gaussian distributed:

**Theorem:** The sum of many independent random variables (regardless of their individual distributions) approaches a normal distribution.

**Application to Random Walks:**
- Each position is the sum of many independent steps
- After sufficient steps, position distribution becomes Gaussian
- This holds even if individual steps are NOT normally distributed
- Verified in Example 6 using uniform and exponential step distributions

**Mathematical Form:**
For n steps with mean μ and variance σ²:

**P(x,t) = (1/√(4πDt)) exp(-x²/(4Dt))**

This is the **diffusion equation solution** for an initial point source.

---

## Examples in the Notebook

The notebook contains 11 comprehensive examples:

### Example 1: Single Symmetric Random Walk
- **Purpose:** Visualize a single walker trajectory
- **Theory demonstrated:** Basic random walk behavior, no drift
- **Key parameter:** `mu=0` (symmetric)

### Example 2: Multiple Random Walks (Ensemble)
- **Purpose:** Show variability between individual walks
- **Theory demonstrated:** Ensemble averaging, statistical nature of walks
- **Key function:** `simulate_ensemble()`

### Example 3: Mean-Square Displacement vs Time
- **Purpose:** Verify ⟨x²⟩ ∝ t relationship
- **Theory demonstrated:** Linear growth of MSD, Einstein relation
- **Visualization:** MSD plot with theoretical prediction

### Example 4: Spatial Distribution at Different Times
- **Purpose:** Show evolution of walker distribution
- **Theory demonstrated:** Gaussian spreading, √t width growth
- **Statistical test:** Comparison with theoretical Gaussian

### Example 5: Biased Random Walk
- **Purpose:** Demonstrate drift (μ ≠ 0)
- **Theory demonstrated:** Combination of drift and diffusion
- **Key insight:** ⟨x(t)⟩ = μt (linear drift), spread still grows as √t

### Example 6: Central Limit Theorem
- **Purpose:** Show CLT applies to any step distribution
- **Theory demonstrated:** Universality of Gaussian limit
- **Step distributions tested:** Uniform, Exponential, Normal

### Example 7: 2D Random Walk
- **Purpose:** Visualize walks in two dimensions
- **Theory demonstrated:** 2D trajectory visualization
- **Key function:** `random_walk_2d()`

### Example 8: 2D Random Walk Ensemble
- **Purpose:** Verify ⟨r²⟩ = 4Dt in 2D
- **Theory demonstrated:** Diffusion in higher dimensions
- **Comparison:** Factor of 4 vs 2 in 1D

### Example 9: 2D Spatial Distribution Over Time
- **Purpose:** Visualize spreading of 2D ensemble
- **Theory demonstrated:** Circular spreading from point source
- **Visualization:** Snapshots at multiple times

### Example 10: Diffusion Time Scaling
- **Purpose:** Show τ ∝ ℓ² (time to reach distance ℓ)
- **Theory demonstrated:** Diffusive scaling, first-passage time
- **Key result:** Time to travel distance ℓ scales as ℓ², not ℓ

### Example 11: Animated Random Walk
- **Purpose:** Create dynamic visualization
- **Theory demonstrated:** Real-time walk evolution
- **Feature:** Interactive Plotly animation

---

## Applications in Environmental Science

Random walks are fundamental to many environmental processes:

### 1. **Pollutant Dispersion**
- Air pollutants undergo random motion due to turbulent eddies
- Water pollutants disperse via molecular and turbulent diffusion
- Models: Advection-diffusion equation combines drift (wind/current) with diffusion

### 2. **Animal Movement and Foraging**
- **Lévy flights:** Modified random walks with heavy-tailed step distributions
- Optimal foraging strategies in patchy environments
- Movement ecology and habitat selection

### 3. **Molecular Diffusion**
- Oxygen, CO₂, and nutrient transport in soils and water
- Biochemical reactions in environmental systems
- Pore-scale transport in porous media

### 4. **Sediment Transport**
- Particle motion in rivers and coastal environments
- Bedload transport as a random process
- Deposition and erosion patterns

### 5. **Climate and Weather**
- Stochastic models of climate variability
- Temperature fluctuations as random walks
- Precipitation patterns

### 6. **Ecosystem Dynamics**
- Population fluctuations
- Disease spread
- Genetic drift in populations

---

## References and Further Reading

### Books
1. **Berg, H. C.** (1993). *Random Walks in Biology*. Princeton University Press.
   - Excellent introduction to biological applications

2. **Redner, S.** (2001). *A Guide to First-Passage Processes*. Cambridge University Press.
   - Comprehensive treatment of first-passage times

3. **Van Kampen, N. G.** (2007). *Stochastic Processes in Physics and Chemistry*. Elsevier.
   - Advanced theoretical treatment

### Papers
1. **Einstein, A.** (1905). "On the movement of small particles suspended in stationary liquids required by the molecular-kinetic theory of heat." *Annalen der Physik*.
   - Original paper connecting random walks to diffusion

2. **Viswanathan, G. M., et al.** (1999). "Optimizing the success of random searches." *Nature*, 401(6756), 911-914.
   - Lévy flights and optimal foraging

3. **Codling, E. A., Plank, M. J., & Benhamou, S.** (2008). "Random walk models in biology." *Journal of the Royal Society Interface*, 5(25), 813-834.
   - Review of biological applications

### Online Resources
1. **Interactive Random Walk Visualizations:** https://www.complexity-explorables.org/
2. **Python Simulations:** https://scipy-lectures.org/
3. **Environmental Applications:** USGS models for pollutant transport

---

## Additional Notes

### Extending the Notebook

Users can extend the examples by:

1. **Implementing 3D random walks** - Extension of 2D code
2. **Adding boundary conditions** - Reflecting or absorbing boundaries
3. **Incorporating correlations** - Persistent random walks (momentum)
4. **Non-Markovian walks** - Memory effects
5. **External fields** - Position-dependent drift

### Performance Considerations

For large ensembles or long simulations:
- Use vectorized NumPy operations (avoid Python loops)
- Consider using Numba JIT compilation
- For very large simulations, use the analytical solutions when possible

### Contributing

To contribute improvements or additional examples:
1. Fork the repository
2. Create a new branch
3. Add your modifications
4. Submit a pull request with clear documentation

---

**Document Version:** 1.0  
**Last Updated:** January 2026  
**Notebook Version:** random_walk.ipynb  
**Author:** Environmental Complex Systems Team
