FROM ubuntu:16.04

MAINTAINER Obscuritylabs
LABEL version="1.0"
LABEL description="Dockerfile for ffmpeg fuzzing."

# docker hardcoded sh...
SHELL ["/bin/bash", "-c"]

# env setup
ENV DEBIAN_FRONTEND=noninteractive

# install proper tools
RUN apt-get update && \
    apt-get install -yq net-tools sudo nano htop

RUN sudo apt-get update -qq && sudo apt-get -y install \
    autoconf \
    automake \
    build-essential \
    cmake \
    git-core \
    libass-dev \
    libfreetype6-dev \
    libsdl2-dev \
    libtool \
    libva-dev \
    libvdpau-dev \
    libvorbis-dev \
    libxcb1-dev \
    libxcb-shm0-dev \
    libxcb-xfixes0-dev \
    pkg-config \
    texinfo \
    wget \
    zlib1g-dev \
    yasm \
    nasm \
    libx264-dev \ 
    libx265-dev \
    libnuma-dev \
    libvpx-dev \ 
    libfdk-aac-dev \ 
    libmp3lame-dev \ 
    libopus-dev \
    python3 \
    python3-pip \
    python2.7 \
    python-pip \
    screen 

# install pip / update
RUN pip install --upgrade pip && pip3 install --upgrade pip

# Install AFL
RUN git clone https://github.com/mirrorer/afl && \
    cd afl && \
    make -j12 && sudo make install

# Install AFL Ecploitable
RUN git clone https://gitlab.com/rc0r/exploitable.git && \ 
    apt install -y gdb && \     
    cd exploitable && python setup.py install

# Install AFL tools
RUN git clone https://gitlab.com/rc0r/afl-utils.git && \
    cd afl-utils && python setup.py install

# Install FFMPEG
RUN mkdir -p ~/ffmpeg_sources ~/bin && \
    cd ~/ffmpeg_sources && \
    wget -O ffmpeg-snapshot.tar.bz2 https://ffmpeg.org/releases/ffmpeg-snapshot.tar.bz2 && \
    tar xjvf ffmpeg-snapshot.tar.bz2 && \
    cd ffmpeg && \
    PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure \
     --cc=afl-gcc \
     --cxx=afl-g++ \
     --prefix="$HOME/ffmpeg_build" \
     --pkg-config-flags="--static" \
     --extra-cflags="-I$HOME/ffmpeg_build/include" \
     --extra-ldflags="-L$HOME/ffmpeg_build/lib" \
     --extra-libs="-lpthread -lm" \
     --bindir="$HOME/bin" \
     --enable-gpl \
     --enable-libass \
     --enable-libfdk-aac \
     --enable-libfreetype \
     --enable-libmp3lame \
     --enable-libopus \
     --enable-libvorbis \
     --enable-libvpx \
     --enable-libx264 \
     --enable-libx265 \
     --enable-nonfree && \
   PATH="$HOME/bin:$PATH" make -j12 && \
   make install && \
   hash -r
ENTRYPOINT ["tail", "-f", "/dev/null"]
