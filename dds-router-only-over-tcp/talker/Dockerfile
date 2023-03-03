# ROS Distribution (ex: melodic, foxy, etc.)
ARG ROS_DISTRO=foxy
FROM ros:${ROS_DISTRO}

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get clean
RUN apt-get update && apt-get install -y \
    lsb  \
    unzip \
    wget \
    curl \
    xterm \
    devilspie \
    xfce4-terminal \
    vim \
    nmap

RUN apt-get install -y ros-foxy-rmw-fastrtps-cpp
RUN apt-get install -y ros-foxy-desktop
ENV HOSTNAME=robot
ENV QT_X11_NO_MITSHM=1

RUN . /opt/ros/foxy/setup.sh

RUN apt-get install -y openssh-server
RUN systemctl enable ssh
#RUN systemctl start ssh
ENV RMW_IMPLEMENTATION=rmw_fastrtps_cpp
#ENV ROS_DISCOVERY_SERVER="10.0.18.239:11811"
WORKDIR /home
RUN echo 'export RMW_IMPLEMENTATION=rmw_fastrtps_cpp' >> /root/.bashrc
RUN echo 'source /opt/ros/foxy/setup.bash ' >> /root/.bashrc

# INSTALL FASTDDS 2.9.1
RUN apt-get install -y cmake g++ python3-pip wget git

RUN apt-get install -y  libasio-dev libtinyxml2-dev
RUN apt-get install -y libssl-dev  python3-pip libyaml-cpp-dev
RUN python3 -m pip install --upgrade pip && python3 -m pip install colcon-common-extensions vcstool
RUN mkdir -p /home/DDS-Router/src
WORKDIR /home/DDS-Router
RUN wget https://raw.githubusercontent.com/eProsima/DDS-Router/main/ddsrouter.repos
RUN vcs import src < ddsrouter.repos

RUN colcon build

RUN . /home/DDS-Router/install/setup.sh

#
COPY ./dds-router-talker.yaml /home/dds-client.yaml
COPY ./fastdds-talker.xml /home/dds-client.xml
ENV FASTRTPS_DEFAULT_PROFILES_FILE=/home/dds-client.xml

WORKDIR /

# Add the application source file to the entrypoint.
RUN echo  "#!/bin/bash \n\
set -e \n\
export ROS_DOMAIN_ID=0 \n\
export RMW_IMPLEMENTATION=rmw_fastrtps_cpp \n\
export ROS_DISCOVERY_SERVER=\"10.0.18.239:9843\" \n\
export FASTRTPS_DEFAULT_PROFILES_FILE=/home/dds-client.xml  \n\
source /opt/ros/foxy/setup.bash \n\
source /home/DDS-Router/install/setup.bash \n\
ddsrouter -c /home/dds-client.yaml & \n\
source /root/.bashrc \n" > /entrypoint.sh
RUN echo 'exec "$@" ' >> /entrypoint.sh
RUN cat /entrypoint.sh
RUN sudo chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
                                   