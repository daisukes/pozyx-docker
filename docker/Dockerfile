from ubuntu:20.04

RUN apt update && apt install -y \
	unzip \
	fuse \
	libfuse2 \
	libgtk2.0-0 \
	libnss3 \
	libgtk-3-0 \
	libx11-xcb1 \
	libasound2 \
	libcanberra-gtk3-module \
	mesa-utils \
	net-tools \
	xserver-xorg-video-all \
	sudo

RUN mkdir /opt

COPY Linux_Creator_Controller.zip Linux_Creator_Controller.zip 

RUN unzip Linux_Creator_Controller.zip 

RUN chmod +x 'Pozyx Creator Controller-2.1.0.AppImage'
RUN chmod +x Binaries/*

ENV USERNAME developer

# Replace 1000 with your user/group id
ARG UID=1000
RUN useradd -m $USERNAME && \
        echo "$USERNAME:$USERNAME" | chpasswd && \
        usermod --shell /bin/bash $USERNAME && \
	usermod -aG sudo $USERNAME && \
        mkdir -p /etc/sudoers.d/ && \
        echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/$USERNAME && \
        chmod 0440 /etc/sudoers.d/$USERNAME && \
        usermod  --uid $UID $USERNAME && \
	groupmod --gid $UID $USERNAME

USER $USERNAME

ENV HOME /home/$USERNAME

WORKDIR $HOME
