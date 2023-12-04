FROM ros:foxy as dev

ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /root/ros2_ws/

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 4B63CF8FDE49746E98FA01DDAD19BAB3CBF125EA

RUN apt-get update && \
    apt-get install -qq -y --no-install-recommends \
    build-essential \
    cmake \
    git \
    libssl-dev \
    libusb-1.0-0-dev \
    pkg-config \
    libgtk-3-dev \
    libglfw3-dev \
    libgl1-mesa-dev \
    libglu1-mesa-dev \    
    libusb-1.0-0 \
    udev \
    apt-transport-https \
    ca-certificates \
    curl \
    vim \
    swig \
    software-properties-common \
    python3-pip \
    ros-foxy-joint-state-publisher-gui \
    ros-foxy-rqt-robot-steering \
    ros-foxy-teleop-twist-keyboard\
    ros-foxy-cartographer-ros \
    ros-foxy-navigation2 \
    ros-foxy-nav2-bringup \
    ros-foxy-rviz2 \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/YDLIDAR/YDLidar-SDK.git &&\
    mkdir -p YDLidar-SDK/build && \
    cd YDLidar-SDK/build &&\
    cmake ..&&\
    make &&\
    make install &&\
    cd .. &&\
    pip install . &&\
    cd .. && rm -r YDLidar-SDK 

RUN mkdir -p /root/ros2_ws/src/ && \
    . /opt/ros/foxy/setup.sh && \
    cd /root/ros2_ws/src && \
    git clone -b foxy https://github.com/agilexrobotics/limo_ros2.git && \
    cd /root/ros2_ws && \
    colcon build && \
    bash /root/ros2_ws/install/setup.bash

RUN echo "source /opt/ros/foxy/setup.bash" >> /etc/bash.bashrc && \
    echo "source /root/ros2_ws/install/setup.bash" >> /etc/bash.bashrc



