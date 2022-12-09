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
        zip \
        libtbb-dev \
        libboost-all-dev \
        cmake \
        cpio \
        python-wstool \
        gedit

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

RUN cd /tmp && \
    wget https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB && \
    apt-key add GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB && \
    wget https://apt.repos.intel.com/setup/intelproducts.list -O /etc/apt/sources.list.d/intelproducts.list
RUN apt-get update && \
    apt-get install -y \
        intel-mkl-2020.0-088

RUN git clone https://bitbucket.org/gtborg/gtsam.git && \
    cd gtsam && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make install

USER ubuntu