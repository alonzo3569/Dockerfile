# Kudos to DOROWU for his amazing VNC 18.04 KDE image
FROM dorowu/ubuntu-desktop-lxde-vnc:xenial

####################################
#            Debian pkg            #        
####################################
RUN apt-get update && apt-get install -y vim \
terminator 


####################################
#              ROS                 #    
####################################

# for apt-key
RUN apt-get update && apt-get install -y dirmngr

# update source list and keyserver
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
#RUN curl -sSL 'http://keyserver.ubuntu.com/pks/lookup?op=get&search=0xC1CF6E31E6BADE8868B172B4F42ED6FBAB17C654' | sudo apt-key add -
# apt-key adv --keyserver 'hkp://pgp.mit.edu:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# apt-get update again after changing source list and key
RUN apt-get update && apt-get install -y ros-kinetic-desktop-full

# add path to .bashrc
RUN echo "source /opt/ros/kinetic/setup.bash" >> /root/.bashrc

# dependencies for building ros pkgs
RUN apt-get install -y python-rosdep \ 
python-rosinstall \
python-rosinstall-generator \
python-wstool build-essential 

# rosdep init 
RUN rosdep init
RUN rosdep update



