# Numerical Optimization – Six Laboratory Notebooks

Author: Andrea Di Via  
University: Università di Genova — Department of Mathematics  
Instructors: Silvia Villa, Emanuele Naldi & Marco Rando

## Overview

This repository collects six laboratory notebooks exploring numerical optimization methods, from classical gradient descent to proximal, accelerated, primal-dual, and stochastic algorithms.

The notebooks combine mathematical background, algorithm implementations, numerical experiments, and visual analysis of convergence.

Applications include:

- Quadratic optimization.
- Overdetermined and underdetermined least squares.
- Nonsmooth convex minimization.
- Constrained optimization.
- Sparse signal reconstruction.
- Total variation image denoising.
- Low-rank matrix completion.
- Linear regression.

The collection follows a progression from smooth deterministic optimization to structured nonsmooth problems and stochastic methods.

## Notebooks at a Glance

| Lab | Topic | Main methods | Applications |
|---|---|---|---|
| 1 | Gradient descent | Fixed-step gradient descent | Quadratic functions and least squares |
| 2 | Subgradient methods | Constant, normalized, and diminishing steps | Absolute-value and piecewise-linear objectives |
| 3 | Proximal methods and acceleration | Projected gradient, proximal gradient, Nesterov, Heavy Ball, ISTA/FISTA | Constrained least squares and LASSO |
| 4 | Image denoising | Dual forward-backward and accelerated dual optimization | Total variation regularization |
| 5 | Matrix completion and primal-dual optimization | Singular-value thresholding, ISTA/FISTA, dual gradient, primal-dual splitting | Matrix recovery from partial observations |
| 6 | Stochastic optimization | GD, SGD, and mini-batch gradient descent | Quadratic objectives and linear regression |

## Laboratory 1 – Gradient Descent

The first notebook studies gradient descent for smooth convex objectives:

```math
x_{k+1}=x_k-\gamma\nabla f(x_k)
```

The experiments investigate how the step size and the geometry of the objective influence the optimization trajectory.

### Case studies

- A two-dimensional quadratic function with adjustable anisotropy.
- Overdetermined least-squares problems.
- Underdetermined least-squares problems.

The least-squares objective is:

```math
f(x)=\frac{1}{2}\|Ax-y\|_2^2
```

### Main experiments

- Compare different fixed step sizes.
- Plot objective values and iterate trajectories.
- Examine distances to reference solutions.
- Relate observed behavior to the spectrum of the quadratic Hessian.
- Investigate oscillation and nonconvergence near limiting step sizes.

The notebook highlights the importance of choosing a step size that matches the smoothness and conditioning of the problem.

## Laboratory 2 – Subgradient Methods

The second notebook extends optimization to convex objectives that are not differentiable everywhere.

The update uses a selected subgradient:

```math
x_{k+1}=x_k-\gamma_k g_k,\qquad g_k\in\partial f(x_k)
```

### Case studies

A weighted absolute-value objective:

```math
f(x)=5|x_1|+2|x_2|
```

A piecewise-linear convex objective:

```math
f(x)=\max_{1\leq i\leq m}(a_i^Tx+b_i)
```

### Step-size strategies

- Constant step size.
- Constant step length through subgradient normalization.
- Diminishing step sizes, including an inverse-square-root schedule.

Because the objective may increase between iterations, the notebook also tracks the best value observed:

```math
f_{\mathrm{best}}^{(k)}=\min_{0\leq i\leq k}f(x_i)
```

The experiments compare oscillations, progress toward low objective values, and sensitivity to step-size parameters.

## Laboratory 3 – Proximal Methods and Acceleration

The third notebook studies composite optimization problems:

```math
\min_x F(x)=f(x)+g(x)
```

Here, the smooth term is handled through a gradient step and the nonsmooth term through a proximal operator.

The proximal-gradient update is:

```math
x_{k+1}=\mathrm{prox}_{\gamma g}\left(x_k-\gamma\nabla f(x_k)\right)
```

### Topics

- Proximal operators.
- Projected gradient for constrained optimization.
- Nesterov Accelerated Gradient.
- Heavy Ball momentum.
- Proximal-gradient and accelerated proximal-gradient methods.

### Case studies

#### Constrained least squares

The notebook minimizes a quadratic objective over a box constraint:

```math
C=[-2,2]^d
```

The proximal operation becomes projection onto the feasible set.

#### Accelerated least squares

Gradient descent, Nesterov acceleration, and Heavy Ball are compared on a quadratic problem.

#### Sparse signal reconstruction

The LASSO model combines a least-squares data term with an L1 penalty:

```math
\min_x \frac{1}{2}\|Ax-\tilde{y}\|_2^2+\lambda\|x\|_1
```

The experiments examine convergence behavior and the role of acceleration in structured optimization.

## Laboratory 4 – Total Variation Image Denoising

The fourth notebook applies convex optimization to image restoration.

Given a noisy image `y`, the objective is:

```math
\min_x \frac{1}{2}\|x-y\|_F^2+\lambda\,\mathrm{TV}(x)
```

The total variation term uses the discrete image gradient:

```math
\mathrm{TV}(x)=\sum_{i,j}\|(\nabla x)_{i,j}\|_2
```

### Main components

- Discrete gradient and divergence operators.
- Dual formulation of the denoising problem.
- Projection-based dual forward-backward iterations.
- Accelerated dual optimization using FISTA.
- Primal-dual gap monitoring.

### Experiments

- Compare reconstructed images for different regularization strengths.
- Examine the trade-off between noise removal and detail preservation.
- Compare standard and accelerated optimization.
- Track primal and dual objective values.

The notebook demonstrates how a dual formulation makes the TV-regularized problem accessible through simple projection operations.

## Laboratory 5 – Matrix Completion and Primal-Dual Optimization

The fifth notebook addresses matrix recovery from partial observations.

The primary regularized model is:

```math
\min_X \frac{1}{2}\|\Phi_I(X)-y\|_2^2+\lambda\|X\|_*
```

Here:

- `Phi_I` selects the observed entries.
- `y` contains the available measurements.
- The nuclear norm promotes low-rank structure.

The nuclear norm is the sum of singular values:

```math
\|X\|_*=\sum_i\sigma_i(X)
```

### Main topics

- Sampling operators and their adjoints.
- Singular-value decomposition.
- Nuclear-norm proximal operators.
- Singular-value thresholding.
- ISTA and FISTA.
- Gradient optimization of a dual formulation.
- Primal-dual splitting for composite objectives.

### Experiments

- Reconstruct synthetic matrices from incomplete noisy observations.
- Compare accelerated and nonaccelerated methods.
- Monitor reconstruction and observation residuals.
- Investigate the effect of regularization and iteration count.

The notebook also introduces the saddle-point perspective underlying primal-dual algorithms.

## Laboratory 6 – Stochastic and Mini-Batch Gradient Descent

The final notebook compares deterministic and stochastic approaches to finite-sum optimization:

```math
F(x)=\frac{1}{n}\sum_{i=1}^{n}f_i(x)
```

### Compared methods

- Full gradient descent: uses the complete dataset at each update.
- Stochastic gradient descent: uses one sampled observation.
- Mini-batch gradient descent: averages gradients over a sampled subset.

For a mini-batch `B_k`, the update is:

```math
x_{k+1}=x_k-\gamma_k\frac{1}{|B_k|}\sum_{i\in B_k}\nabla f_i(x_k)
```

### Case studies

- A synthetic quadratic finite-sum objective.
- Linear regression with synthetic data:

```math
\min_w \frac{1}{2n}\|Xw-Y\|_2^2
```

### Experiments

- Compare constant and diminishing learning rates.
- Vary the batch size.
- Observe fluctuations in stochastic trajectories.
- Compare objective values and distances to reference solutions.

The notebook explores the trade-off between the cost of an update and the stability of the optimization process.

## Shared Experimental Themes

Across the six notebooks, the experiments examine:

- Step-size selection.
- Smoothness and strong convexity.
- Conditioning of quadratic objectives.
- Nonsmooth regularization.
- Projection and proximal operators.
- Momentum and acceleration.
- Primal and dual formulations.
- Sensitivity to initialization.
- Deterministic versus stochastic updates.
- Numerical precision and stopping criteria.

The figures provide a practical connection between mathematical assumptions and observed algorithm behavior.

## How to Use This Repository

1. Clone or download the repository.
2. Open the notebooks in the environment matching their file format.
3. Install or enable the dependencies imported by each notebook.
4. Ensure that any required image assets or supporting files are available.
5. Execute each notebook from the beginning to initialize its data and parameters.
6. Modify the experimental settings to compare alternative configurations.

The recommended reading order is Laboratory 1 through Laboratory 6.

The later notebooks build on concepts introduced earlier, particularly gradient descent, convexity, proximal operators, and duality.

## Data and Dependencies

Most case studies use synthetic matrices, vectors, signals, or regression datasets.

The image-denoising notebook additionally requires the image used in its experiments.

Exact package requirements, notebook formats, and asset paths should be checked in the notebook imports and data-loading cells.

## Reproducibility

For reproducible comparisons:

- Fix random seeds where random data or sampling is used.
- Run notebooks from a clean execution state.
- Record step sizes, regularization parameters, and iteration limits.
- Compare methods on the same generated problem instance.
- Preserve the required input assets.

Random initialization and stochastic sampling may produce different curves across executions.

## Interpreting the Results

The experiments are educational demonstrations rather than comprehensive performance benchmarks.

When comparing methods:

- Distinguish convergence to an optimization solution from recovery of the original signal or matrix.
- Remember that regularization changes the objective and may introduce reconstruction bias.
- Do not infer universal superiority from one synthetic experiment.
- Compare computational work as well as iteration counts: GD, SGD, and mini-batch updates have different costs.
- Interpret very small residual fluctuations in light of floating-point precision.
- Check the assumptions required by theoretical convergence statements.

Observed behavior depends on the problem instance, parameter choices, and stopping conditions.

## Learning Objectives

The collection aims to develop an understanding of how to:

- Match optimization algorithms to objective structure.
- Implement and analyze first-order methods.
- Handle constraints and nonsmooth penalties.
- Use acceleration appropriately.
- Formulate dual and primal-dual algorithms.
- Apply optimization to imaging and matrix recovery.
- Evaluate stochastic optimization trade-offs.
- Connect numerical experiments with mathematical theory.

## Author and Academic Context

These laboratories were prepared by Andrea Di Via at the Department of Mathematics, Università di Genova.

The accompanying reports identify Silvia Villa, Emanuele Naldi, and Marco Rando as instructors.

---

Numerical Optimization – Laboratory Notebooks  
Andrea Di Via — Università di Genova