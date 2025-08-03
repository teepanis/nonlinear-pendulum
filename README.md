<h1 align="center">Supplemental Material</h1>
<h2 aligne="center">Exact frequency-domain solutions for nonlinear pendulum-like dynamics</h2>
Teepanis Chachiyo <teepanisc@nu.ac.th>, Department of Physics, Faculty of Science, Naresuan University, Phitsanulok 65000, Thailand.


## File List
1. **supplemental_material.ipynb**: Python notebook producing the results and figures in the paper
2. **simple_example.ipynb**: simple and minimal example of ploting the exact solution 
3. **animation.ipynb**: Python notebook generating GIF animation using the derived exact solutions
4. **nonlinear_motion.gif**: GIF animation showing the 3 classes of motions

<br>
The research article preprint >> <a href="https://arxiv.org/abs/2504.16816">https://arxiv.org/abs/2504.16816</a>

## Abstract
Beyond classical physics, pendulum-like dynamics arise in diverse systems, such as superconducting Josephson junctions, Bose-Einstein condensates tunneling, and emerging artificial intelligence models for nonlinear pattern recognition. While the nonlinear pendulum admits long-standing exact solutions in terms of Jacobi elliptic functions, they do not reveal the frequency content of the motion. Consequently, studies of pendulum-like dynamics must rely on perturbative, approximate, or numerical methods to characterize their oscillatory behavior. Here, we present complete, exact, and closed-form frequency-domain solutions for the energy-conserving nonlinear pendulum across all initial conditions and regimes: swinging, stopping, and spinning. These solutions are derived through angular-velocity frequency analysis and expressed in terms of elementary functions. Their accuracy is validated by agreement with numerical values to machine precision and by frequency analysis of dynamical simulations performed using Velocity Verlet integration. A comparison with the perturbation method is presented. Applications to quantum analogues are also discussed.

<br>
<br>
<center><img src="graphical_abstract.gif" width="540"  alt="Pendulum Motion"></center>
<center><img src="nonlinear_motion.gif" width="540"  alt="3 Classes of Nonlinear Pedulum Motion"></center>

## Citation

In the meantime, if you use any part of this repository please cite the following preprint:

```
@article{Chachiyo:2025sae,
    author = "Teepanis Chachiyo",
    title = "{Exact frequency-domain solutions for nonlinear pendulum-like dynamics}",
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
