FROM osrf/ros:noetic-desktop-full


RUN apt update && apt-get upgrade -y
RUN rosdep update
RUN apt update && apt-get upgrade -y
RUN apt install -y ros-noetic-catkin python3-catkin-tools python3-osrf-pycommon 
RUN apt install python3-wstool
RUN apt install -y git

RUN mkdir -p ~/ws_moveit/src
RUN /bin/bash -c "cd ~/ws_moveit/src; wstool init .; wstool merge -t . https://raw.githubusercontent.com/ros-planning/moveit/master/moveit.rosinstall; wstool remove moveit_tutorials; wstool update ."
RUN /bin/bash -c "git clone https://github.com/ros-planning/moveit_tutorials.git -b master;git clone https://github.com/ros-planning/panda_moveit_config.git -b noetic-devel"

RUN /bin/bash -c "cd ~/ws_moveit/src ;rosdep install -y --from-paths . --ignore-src --rosdistro noetic"
RUN /bin/bash -c "cd ~/ws_moveit;catkin config --extend /opt/ros/${ROS_DISTRO} --cmake-args -DCMAKE_BUILD_TYPE=Release; catkin build"
RUN echo "source ~/ws_moveit/devel/setup.bash" >> ~/.bashrc

