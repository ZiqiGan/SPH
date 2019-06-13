## UCSD CSE 291D  SP19
#### Author: Ziqi Gan
#### Project: Particle Based Fluids

## Features
This project implements:
### Basic SPH Solver
- Algorithm 1 from "SPH Fluids in Computer Graphics"
- Calulate pressure force explicitly with state equations.
```
For all particles:
  Find neighbors
For all particles:
  compute density
For all particles:
  compute presssure force
  compute viscosity force
  compute other forces (e.g. gravity)
  Add them up
For all particles:
  update velocity
  update position
```
- Pros: Easy to implement.
- Cons: 
  * Unstable
  * Small time step.
### Acceleration Structure
For faster neighborhood search I implemented a uniform grid.  
- The simulation space is divided into small cubic cells.
- Each particle is associated with one of the cells. 
- The cell length equals to the support radius of the kernel. 
- For each particle, loop through 3^3 = 27 cells to find all its neighbors.
### Divergence Free Solver
- Solve pressure force implicitly.
- Predict particle velocities with non-pressure forces and iteratively correct density and divergence error.
- Divergence free solver is used to correct velocity field.
- Constant density solver to correct numerical errors.
- Simulation Step:
```
For all particles:
  find neighbors
For all particles:
  calculate densities and some factors

while(t < t_max):
  For all particles:
    calculate non-pressure forces.
  calculate adaptive time step using CFL condition
  For all particles:
    predict velocities with calculated time step
  correct density error
  For all particles:
    predict position
  For all particles:
    find neighbors
  For all particles:
    calulate densities and some factors
  For all particles:
    correct divergence error
  For all particles:
    update velocities
```
- Pros:
  * Stable
  * Adaptive time step for faster update
- Cons:
  * Difficult to implement. Have to set up initial conditions carefully.
  
### High Viscosity Fluid
The DFSPH paper also introduces an implicit viscosity solver.
- Viscosity tensor is defined by the strain rate tensor adn the viscosity coefficient.
- Similar approach as the divergence and density solver.
- Iteratively compute the predicted strain rate, comparing it with the target strain rate, and correct velocities.
- Pros: Easy to intergrate with the divergence free solver.
- Cons:
  * Viscosity parameter depends on the time step. Not physically meaningful.
  * Solving the inverse of a six-dimentional matrix for each constriant, causing a large computional effort.
  * Extremely difficult to set up initial conditions.
    + Fixed time step: 1ms
    + particle radius: 0.025m
    
<a href="http://www.youtube.com/watch?feature=player_embedded&v=9aFXjCeBRfM
" target="_blank"><img src="http://img.youtube.com/vi/9aFXjCeBRfM/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>

### Air-Fluid Interaction

## External Libraries
1. OpenGL Bindings: [GLEW](http://glew.sourceforge.net/), [GLFW](https://www.glfw.org/) . 
2. Math: [GLM](https://glm.g-truc.net/0.9.9/index.html), [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page) . 
3. Search: [CompactNSearch](https://github.com/InteractiveComputerGraphics/CompactNSearch) . 
4. GUI: [AntTweakBar](http://anttweakbar.sourceforge.net/doc/) . 
5. Parallelism: [OpenMP](https://www.openmp.org/) . 

## References
- "SPH Fluids in Computer Graphics", Ihmsen, Orthmann, Solenthaler, Kolb, Teschner
- Jan Bender and Dan Koschier. Divergence-free SPH for incompressible and viscous fluids. IEEE Transactions on Visualization and Computer Graphics, 2017.
- Miles Macklin, Matthias Müller, Nuttapong Chentanez and Tae-Yong Kim. Unified Particle Physics for Real-Time Applications. ACM Trans. Graph., 33(4), 2014

## Videos
