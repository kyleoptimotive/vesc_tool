FROM ubuntu:22.04

ENV TZ=America/New_York
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y \
    git \
    make \
    g++ \
    wget \
    zip \
    qtdeclarative5-dev \
    qtquickcontrols2-5-dev \
    libqt5svg5-dev \
    qtpositioning5-dev \
    libqt5serialport5-dev \
    libqt5gamepad5-dev \ 
    qtbase5-private-dev \
    qtconnectivity5-dev \
    gcc-arm-none-eabi \
    libnewlib-arm-none-eabi \
    && rm -rf /var/lib/apt/lists/*

RUN cd /tmp && \
    # clone the VESC Firmware and VESC Tool repos
    git clone https://github.com/vedderb/bldc.git && \
    git clone https://github.com/vedderb/vesc_tool.git

# Install the ARM GCC SDK
RUN cd /tmp/bldc && \
    make arm_sdk_install

# Build the VESC Firmware and VESC Tool executable
RUN cd /tmp/vesc_tool && \
    # In './build_cp_fw' modify the 'FWPATH' variable to point to the top of the 'bldc' repository.
    sed -i 's|FWPATH=.*|FWPATH=/tmp/bldc|' build_cp_fw && \
    # build the VESC Firmware to generate '/res/firmwares/res_fw.qrc' to be used with VESC Tool
    chmod +x build_cp_fw && \
    ./build_cp_fw && \
    # build the VESC Tool executable
    chmod +x build_lin && \
    ./build_lin
