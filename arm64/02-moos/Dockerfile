FROM arm64v8/ros:melodic

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
RUN echo "PATH=\$PATH:/root/moos-ivp/bin" >> ./.bashrc
