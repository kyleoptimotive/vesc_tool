# Docker Image for VESC Tool on Ubuntu 22.04
The purpose of this Docker image is to provide a consistent and reproducible environment for building and running the VESC Tool on Ubuntu 22.04. This containerized setup ensures that all necessary dependencies are installed and configured correctly, regardless of the host system. It simplifies the process of compiling the VESC Firmware and building the VESC Tool executable, making it easier for developers and users to work with the VESC Tool across different machines.

The Dockerfile performs the following steps:
1. Install package dependencies
2. Clone the VESC Firmware and VESC Tool repos
3. Install the ARM GCC SDK
4. Build the VESC Firmware and VESC Tool executable

# Launching the VESC Tool GUI in Docker
Once inside the container, you can launch the VESC Tool GUI with the following steps:
1. Navigate to `vesc_tool/build/lin` where you should see several .zip files.
2. Extract the desired vesc_tool version from the respective zip file with `unzip <zipfile>`.
3. Once extracted, launch the GUI with `./vesc_tool...`.

# Docker Build Command 
`docker build -t vesc_tool .`

# Docker Run Command
`docker run -it --net=host --env DISPLAY=$DISPLAY vesc_tool`