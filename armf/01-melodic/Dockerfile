FROM ros:melodic-ros-base-bionic

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

