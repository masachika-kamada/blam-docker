FROM osrf/ros:melodic-desktop-full

USER root

# Install X Window System
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y \
        x11-xserver-utils \
        xorg \
        x11-apps \
        git \
        wget \
        zip

RUN adduser ubuntu
ENV HOME=/home/ubuntu
WORKDIR $HOME

# ROSの環境整理
# ROSのセットアップシェルスクリプトを.bashrcファイルに追記
RUN echo "source /opt/ros/melodic/setup.sh" >> .bashrc
RUN mkdir -p catkin_ws/src

ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics

RUN wget https://bitbucket.org/gtborg/gtsam/get/8b0c2ecaf406.zip && \
    unzip 8b0c2ecaf406.zip
RUN cd ./gtborg-gtsam-8b0c2ecaf406 && \
    mkdir build && \
    cd ./build && \
    cmake .. && \
    make install

RUN cd $HOME/catkin_ws/src && \
    git clone https://github.com/erik-nelson/blam.git

# RUN cd $HOME/catkin_ws/src/blam && \
#     ./update && \
#     source $HOME/catkin_ws/devel/setup.bash && \
#     cd .. && \
#     catkin_make_isolated --install --cmake-args -DCMAKE_BUILD_TYPE=Release

USER ubuntu