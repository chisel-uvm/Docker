# Pull base image.
FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive


RUN apt update 								  \
    && apt install -y --no-install-recommends     \ 
	build-essential 							  \
	clang   		\
    bison     \
    flex    \
    libreadline-dev    \
    gawk   \
    tcl-dev   \
    libffi-dev    \
    git    \
    graphviz   \
    xdot  \
    pkg-config   \
    python3   \
    libboost-system-dev   \
    libboost-python-dev   \
    libboost-filesystem-dev   \
    zlib1g-dev    \
    gnat  \
	ca-certificates \
	&& apt clean \
    && rm -rf /var/lib/apt/lists/*


RUN mkdir gittemp \
	&& ls \
	&& cd gittemp \
	&& ls \
	&& git clone --recurse-submodules -j4 https://github.com/chisel-uvm/vhdl2verilog.git \
	&& cd vhdl2verilog \
	&& export MAKEFLAGS=-j$(nproc) \
	&& cd yosys && make && make install && cd ..  \
	&& cd ghdl && ./configure --prefix=/usr/local && make && make install && cd ..  \
	&& cd ghdl-yosys-plugin && make && make install \
	&& cd ../.. && rm -rf gittemp

	
# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["bash"]
