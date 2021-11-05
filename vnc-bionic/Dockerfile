# Kudos to DOROWU for his amazing VNC 18.04 KDE image
FROM dorowu/ubuntu-desktop-lxde-vnc:bionic


####################################
#            Debian pkg            #        
####################################
RUN apt-get update && apt-get install -y vim \
iputils-ping \
net-tools    \
nmap         \
libasound2-dev \
alsa \
python-pip \
python3-pip \
python3-numpy \
python3-matplotlib \
librapidxml-dev \
iperf3 \
terminator \
psmisc 
# iputils-ping for ping
# librapidxml-dev for moos-ros-bridge
# psmisc for killall


####################################
#              ROS                 #    
####################################

# for apt-key
RUN apt-get update && apt-get install -y dirmngr

# update source list and keyserver
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# apt-get update again after changing source list and key
RUN apt-get update && apt-get install -y ros-melodic-desktop-full

# add path to .bashrc
RUN echo "source /opt/ros/melodic/setup.bash" >> /root/.bashrc

# dependencies for building ros pkgs
RUN apt-get install -y python-rosdep \ 
python-rosinstall \
python-rosinstall-generator \
python-wstool build-essential \
ros-melodic-rosserial \
ros-melodic-rosserial-arduino \
ros-melodic-joint-state-publisher-gui \
ros-melodic-joy
# rosserial, rosserial-arduino for arduino
# joint-state-publisher-gui for rviz
# joy for joystick control

RUN python3 -m pip install qbstyles
RUN pip3 install pyyaml rospkg
# qbstyles, pyyaml rospkg for visualization

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
RUN svn co https://oceanai.mit.edu/svn/moos-ivp-aro/trunk/ moos-ivp

# update to latest version
WORKDIR /root/moos-ivp
RUN svn update

# build
WORKDIR /root/moos-ivp
RUN ./build-moos.sh
RUN ./build-ivp.sh

# add path to .bashrc
WORKDIR /root
RUN echo "PATH=\$PATH:/root/moos-ivp/bin:/root/vnc-bionic/moos-ivp-agx/bin" >> ./.bashrc
RUN echo ". /root/vnc-bionic/catkin_ws/devel/setup.bash" >> ./.bashrc
RUN echo "export ROS_MASTER_URI=http://localhost:11311" >> ./.bashrc

RUN rm -rf /var/lib/apt/lists/*
