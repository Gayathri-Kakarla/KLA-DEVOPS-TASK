# KLA-DEVOPS-TASK
# DockerHelper - A PowerShell Docker Management Script

This project provides a PowerShell script (`DockerHelper.ps1`) for managing Docker images and containers, along with the necessary files to build and run a Docker container that calculates Fibonacci numbers.

## Project Structure

DockerProject/
├── Dockerfile               # Docker configuration file to build the image
├── DockerHelper.ps1         # PowerShell script to manage Docker operations
├── fibonacci.py             # Python script to calculate Fibonacci numbers
└── README.txt               # Documentation for the project
 The scripts provided can be aligned with the requirements of the task.

---
    1.Copy necessary files for Docker to a remote or local system.
    2.Build a Docker image. 
    3.Run a Docker container.
---
#### **Step 1: Copy Files to the Remote Machine**

 - It copies files (`-Path`) from your computer to a remote computer (`-ComputerName`) to a specific directory (`-Destination`).
  - This is useful when the Dockerfile or other files needed for the build aren't already on the remote system.

Run the following command to copy files to the remote system:

   Copy-Prerequisites -ComputerName "RemoteHostName" -Path @("Dockerfile", "fibonacci.py") -Destination "C$\DockerBuild"

#### **Step 2: Build the Docker Image**

  - It takes the path to the Dockerfile (`-Dockerfile`), the name of the image to be built (`-Tag`), and the directory containing the Docker context (`-Context`).
  - Optionally, it allows you to specify a remote host (`-ComputerName`). If no host is specified, it runs locally.
  - If you provide a remote computer name, it runs the build command on the remote machine using `Invoke-Command`.
  - If no computer name is provided, it builds the image locally using `docker build`.

Build the Docker image locally or remotely:

   Build-DockerImage -Dockerfile "C:\DockerBuild\Dockerfile" -Tag "fibonacci:latest" -Context "C:\DockerBuild" -ComputerName "RemoteHostName"

   or
   
   Build-DockerImage -Dockerfile "C:\DockerBuild\Dockerfile" -Tag "fibonacci:latest" -Context .

   

#### **Step 3: Run the Docker Container**

To run the container continuously (outputs Fibonacci numbers):

   Run-DockerContainer -ImageName "fibonacci:latest"

To get a specific Fibonacci number (e.g., the 10th number):

   Run-DockerContainer -ImageName "fibonacci:latest" -DockerParams @("-it", "--rm", "10") or 

   Run-DockerContainer -ImageName "fibonacci:latest"  10
