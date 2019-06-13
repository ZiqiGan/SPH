## UCSD CSE 291D  SP19
#### Author: Ziqi Gan
#### Project: Particle Based Fluids

## Features
This project implements:
### Basic SPH Solver
### Acceleration Structure
For faster neighborhood search I implemented a uniform grid.  
- The simulation space is divided into small cubic cells.
- Each particle is associated with one of the cells. 
- The cell length equals to the support radius of the kernel. 
- For each particle, loop through $3^3 = 27$ cells to find all its neighbors.
### Divergence Free Solver
### High Viscosity Fluid
The DFSPH paper also introduces an implicit viscosity solver, 
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
