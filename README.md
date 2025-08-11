# mps_burgers
Matrix product state and operator-accelerated solver of the nonlinear Burgers' equation in Pennylane

Please read the Project_description.pdf

___
Summary of Algorithm:
========

1) Encode the initial condition as a matrix product state (MPS). Owing to the special structure of the discontinuous initial condition, you are guaranteed that a bond dimension of 2, irrespective of the number of qubits yields maximal accuracy. Also, additional MPS compression will be done by finding correlations across similar length scales. See Gourianov et al., Science Advances, 2025
2) Discretise the linear Laplacian term with a second-order accurate central finite difference scheme. 
3) Create the matrix product operator (MPO) representation of the discretise Laplacian scheme using ladder operators, as given by Ripoll, Quantum, 2021; Sato et al., PRR, 2024. Such a scheme is guaranteed to have a bond dimension of 3, suggesting there exists an efficient quantum gate representation. 
4) Discretise the first derivative associated with the nonlinear convection term with a first-order upwind finite difference scheme.
5) Create the matrix product operator (MPO) representation of the first-order upwind scheme
6) Prepare an ancilla registry containing a copy of the amplitude-encoded velocity state vector |v>. Then, apply the MPO of the first-order upwind scheme
7) Either through mid-circuit measurement of the ancilla registry to postselect the all |0> state or through extra control ancillae, apply a Hadamard product operator to implement the nonlinear term
8) Implement an approximate Hamiltonian simulation to evolve the velocity forwards in time.
9) Measure the final velocity state vector.

    
____
Running this package: 
========
To run this package, you require a GPU with CUDA 12 and associated drivers installed on your computer. 

On Windows: 
Install WSL2
Open Visual Studio Code on the Windows-side
Select "Connect to WSL" on the bottom left or through the toolbar at the top
From the bash terminal within Visual Studio Code, create a new conda environment: 
conda create -n my_env_name
conda activate my_env_name

Install the following Python packages inside of your new environment. 
To use pennylane-lightning-tensor, you must have CUDA 12 installed. Newer versions will not be acceptable. If WSL is not accessible, then NVIDIA provides Docker images with CUDA XX installed. 
pip install cutensornet-cu12 
pip install pennylane-lightning-tensor

