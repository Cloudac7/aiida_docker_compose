FROM aiidateam/torquessh_base:1.0
MAINTAINER AiiDA Team <info@aiida.net>

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Install required packages
RUN apt-get update \ 
    && apt-get install -y --no-install-recommends \
    gfortran \
    libblas-dev \
    liblapack-dev \
    build-essential \
    m4 \
    openmpi-bin \
    libopenmpi-dev \
    git \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean all

USER app

WORKDIR /home/app

#
# Compile Yambo; then I also remove the source code 
# and keep only the executables to reduce the size
#
RUN apt-get update \ 
    && apt-get install -y --no-install-recommends \
    
    git clone https://github.com/yambo-code/yambo && \
    cd yambo && \
    git checkout 4.2.0 && \
    ./configure && \
    make yambo ypp p2y && \
    mkdir /home/app/bin/ && \
    cp bin/* /home/app/bin/ && \
    cd ../ && \
    rm -rf yambo

# I need to go back to root
USER root   


    