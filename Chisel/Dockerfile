FROM ubuntu:20.04
# Curl needed for download.
#gnupg needed for installing SBT
#software-properties-common needed for add-apt-repository
RUN apt update \
    && apt install -y curl gnupg software-properties-common make

#Install Java OpenJDK 8
RUN add-apt-repository ppa:openjdk-r/ppa \
	&& apt-get update \
	&& apt-get -y install openjdk-8-jdk

# Install sbt
RUN echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list \
    && curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | apt-key add \
    && apt-get update \
    && apt-get -y install sbt

# Install Verilator
RUN apt update \
    && apt install -y git make autoconf g++ flex bison \
    && git clone http://git.veripool.org/git/verilator	\
    && cd verilator \
    && git pull \
    && git checkout v4.016 \
    && unset VERILATOR_ROOT \ 
    && autoconf \
    && ./configure \
    && make \
    && make install

#Downloads the needed environment the first time
RUN sbt run; exit 0
