FROM arm32v7/ros:melodic-ros-base-bionic

ENV DEBIAN_FRONTEND noninteractive

####################################
#            Debian pkg            #        
####################################
RUN apt update && apt install -y vim \
net-tools \
nmap \
iputils-ping \
psmisc  # killall

####################################
#              ROS                 #    
####################################

# add path to .bashrc
RUN echo "source /opt/ros/melodic/setup.bash" >> /root/.bashrc
RUN echo "source /root/armhf/catkin_ws/devel/setup.bash" >> /root/.bashrc
RUN echo "export ROS_IP=192.168.0.14" >> /root/.bashrc 
RUN echo "export ROS_MASTER_URI=http://192.168.0.78:11311" >> /root/.bashrc

####################################
#              sensor              #    
####################################

# GPS dependencies

# python module serial
RUN apt install -y python-pip 
RUN pip install pyserial 

# IMU dependencies

# module tf
RUN apt install -y ros-melodic-tf
# arduino
RUN apt install -y ros-melodic-rosserial

RUN rm -rf /var/lib/apt/lists/*
