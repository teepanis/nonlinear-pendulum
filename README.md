<h1 align="center">Supplemental Material</h1>
<h2 aligne="center">Simple and exact nonlinear pendulum motion for all possible initial conditions</h2>
Teepanis Chachiyo <teepanisc@nu.ac.th>, Department of Physics, Faculty of Science, Naresuan University, Phitsanulok 65000, Thailand.


## File List
1. **supplemental_material.ipynb**: Python notebook producing the results and figures in the paper
2. **simple_example.ipynb**: simple and minimal example of ploting the exact solution 
3. **animation.ipynb**: Python notebook generating GIF animation using the derived exact solutions
4. **nonlinear_motion.gif**: GIF animation showing the 3 classes of motions

<br>
The research article preprint >> <a href="https://arxiv.org/abs/2504.16816">https://arxiv.org/abs/2504.16816</a>

## Abstract
Despite centuries of investigation, exact solutions describing nonlinear pendulum motion in the frequency domain have remained elusive. Existing formulations, while mathematically exact in the time domain via Jacobi elliptic functions, do not directly yield tractable, closed-form expressions for the frequency content of the motion, limiting both theoretical understanding and practical applications. This work presents complete, exact, and closed-form frequency-domain solutions for energy-conserving nonlinear pendulum motion across all regimes: swinging, stopping, and spinning. These solutions are derived through an angular velocity frequency analysis, and expressed in terms of elementary functions. The exact frequency contents are validated by their agreement with exact numerical values to machine precision, and by frequency analysis of dynamical simulations performed using Velocity Verlet integration. A comparison to the perturbation method is presented. Applications to quantum analogues, such as superconducting Josephson junctions and Bose-Einstein condensate tunneling, are discussed.

<br>
<br>
<center><img src="graphical_abstract.gif" width="540"  alt="Pendulum Motion"></center>
<center><img src="nonlinear_motion.gif" width="540"  alt="3 Classes of Nonlinear Pedulum Motion"></center>

## Citation

In the meantime, if you use any part of this repository please cite the following preprint:

```
@article{Chachiyo:2025sae,
    author = "Teepanis Chachiyo",
    title = "{Simple and exact nonlinear pendulum motion for all possible initial conditions}",
    eprint = "2504.16816",
    archivePrefix = "arXiv",
    primaryClass = "physics.class-ph",
    month = "4",
    year = "2025"
}
```

## 'Hello-World' example for the swinging nonlinear pendulum

```python
# exact solution of nonlinear pendulum via spectral analyis
# https://github.com/teepanis/nonlinear-pendulum
import numpy as np
import scipy as sp
import matplotlib.pyplot as plt

# physics: amplitude, and OmegaL=sqrt(g/L)
theta0 = 179.9/180*np.pi
OmegaL = np.sqrt(9.8/1)

k = np.sin(theta0/2)
T = 4*sp.special.ellipk(k**2)/OmegaL
Omega0 = 2*np.pi/T
kappa = sp.special.ellipk(1-k**2)

t = np.linspace(0,2*T,200)
theta = np.zeros(len(t)) 

# set phase
delta = np.pi/2

# adding odd harmonics 
for n in range(1,40,2):
    a = 4/n/np.cosh(kappa*n*Omega0/OmegaL)
    theta = theta + a*np.sin(n*Omega0*t + n*delta)

plt.plot(t, theta)
plt.grid()
plt.show()
```

To compare with the traditional perspective we:
1. use the initial condition that the pendulum starts at rest, with an amplitude $\\theta_0$.
2. For this condition, the phase in this work is precisely $\\delta = \\pi/2$.
3. For convenience, we use the form $k = \\sin(\\theta_0/2)$, which is equipvalent to $k = \\omega_m/\\omega_c$.
