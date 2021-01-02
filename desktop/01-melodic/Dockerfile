FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive

####################################
#            Debian pkg            #        
####################################
RUN apt-get update && apt-get install -y vim \
terminator \
psmisc  # killall


####################################
#              ROS                 #    
####################################

# for apt-key
RUN apt-get update && apt-get install -y dirmngr

# update source list and keyserver
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros-latest.list'
RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# apt-get update again after changing source list and key
RUN apt-get update && apt-get install -y ros-melodic-desktop-full

# add path to .bashrc
RUN echo "source /opt/ros/melodic/setup.bash" >> /root/.bashrc
RUN echo "source /usr/share/gazebo/setup.sh" >> /root/.bashrc  # gazebo env

# dependencies for building ros pkgs
RUN apt-get install -y python-rosdep \ 
python-rosinstall \
python-rosinstall-generator \
python-wstool build-essential \
ros-melodic-joint-state-publisher-gui # for rviz

# rosdep init 
RUN rosdep init
RUN rosdep update


