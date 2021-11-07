FROM nvcr.io/nvidia/l4t-base:r32.4.4

ENV DEBIAN_FRONTEND noninteractive

####################################
#            Debian pkg            #        
####################################
# net-tools for ifconfig
# iputils-ping for ping
# psmisc for killall 
# librapidxml-dev for moos-ros-bridge

RUN apt update && apt install -y vim \
terminator   \
net-tools    \
nmap         \
iputils-ping \
libasound2-dev \
alsa \
python-pip \
librapidxml-dev \
python-pyaudio \
iperf3 \
psmisc 

####################################
#              ROS                 #    
####################################

# for apt-key
RUN apt update && apt install -y dirmngr

# update source list and keyserver
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros-latest.list'

RUN apt install -y curl
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -

# apt-get update again after changing source list and key
RUN apt update && apt install -y ros-melodic-desktop-full

# add path to .bashrc
RUN echo "source /opt/ros/melodic/setup.bash" >> /root/.bashrc

# dependencies for building ros pkgs
RUN apt install -y python-rosdep \ 
python-rosinstall \
python-rosinstall-generator \
python-wstool build-essential \
ros-melodic-geodesy \
ros-melodic-joint-state-publisher-gui \ 
python3-pip \
python3-numpy \
python3-matplotlib \
python-scipy \
ros-melodic-multimaster-fkie
# joint-state-publisher for rviz
# geodesy for robot localization
# matplotlib for visualization
# scipy for signal_process
# fkie for multimaster

RUN pip3 install pyyaml rospkg


# rosdep init 
RUN rosdep init
RUN rosdep update

####################################
#             MOOS                 #   
####################################

# pkg for building ivp
RUN apt-get install -y g++  cmake  xterm subversion \
ibfltk1.3-dev  freeglut3-dev  libpng-dev  libjpeg-dev \
libxft-dev  libxinerama-dev   libtiff5-dev 

# clone ivp and 
WORKDIR /root
RUN svn co https://oceanai.mit.edu/svn/moos-ivp-aro/trunk/ moos-ivp

# update to latest version
WORKDIR /root/moos-ivp
RUN svn update 

# build
RUN ./build.sh

# add path to .bashrc
WORKDIR /root
RUN echo "PATH=\$PATH:/root/moos-ivp/bin:/root/moos-ivp-agx/bin" >> ./.bashrc
RUN echo ". /root/arm64-nvidia/catkin_ws/devel/setup.bash" >> ./.bashrc
RUN echo "export ROS_IP=192.168.0.100" >> ./.bashrc   
RUN echo "export ROS_MASTER_URI=http://192.168.0.100:11311" >> ./.bashrc
RUN echo "export DISPLAY=:0.0" >> ./.bashrc

RUN rm -rf /var/lib/apt/lists/*
