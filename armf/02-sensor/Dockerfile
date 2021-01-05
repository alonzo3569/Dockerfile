FROM arm32v7/ros:melodic-ros-base-bionic

ENV DEBIAN_FRONTEND noninteractive

####################################
#            Debian pkg            #        
####################################
RUN apt update && apt install -y vim \
psmisc  # killall

####################################
#              ROS                 #    
####################################

# add path to .bashrc
RUN echo "source /opt/ros/melodic/setup.bash" >> /root/.bashrc

####################################
#              sensor              #    
####################################

# GPS dependencies

# python module serial
RUN apt install -y python-pip 
RUN pip install -y pyserial 

# IMU dependencies

# module tf
RUN apt install -y ros-melodic-tf

