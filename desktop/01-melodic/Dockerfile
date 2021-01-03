FROM osrf/ros:melodic-desktop-full-bionic

ENV DEBIAN_FRONTEND noninteractive

####################################
#            Debian pkg            #        
####################################
RUN apt update && apt install -y vim \
terminator \
psmisc  # killall

####################################
#              ROS                 #    
####################################

# add path to .bashrc
RUN echo "source /opt/ros/melodic/setup.bash" >> /root/.bashrc
RUN echo "source /usr/share/gazebo/setup.sh" >> /root/.bashrc  # gazebo env

# dependencies for building ros pkgs
RUN apt install -y ros-melodic-joint-state-publisher-gui # for rviz


