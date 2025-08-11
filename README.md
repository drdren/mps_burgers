# mps_burgers
Matrix product state and operator-accelerated solver of the nonlinear Burgers' equation in Pennylane

Please read the Project_description.pdf

____
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

