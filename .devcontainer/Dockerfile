# Copyright © 2001 by the Rectors and Visitors of the University of Virginia. 

# Extend Ubunto 20.04
FROM ubuntu:20.04

# Create image without any user interaction
ENV DEBIAN_FRONTEND=noninteractive
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

# Update and configure Ubuntu 
RUN apt-get clean && apt-get update -y && apt-get upgrade -y
RUN apt-get install -y locales && locale-gen en_US.UTF-8  
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  
WORKDIR /root  
# COPY .devcontainer/.profile.txt /root/.profile
VOLUME /hostdir

# Install Python3
RUN apt-get update --fix-missing
RUN apt-get -y install lsb-release build-essential git vim wget gnupg curl python3-pip python3-venv python3-dev libssl-dev libffi-dev libconfig-dev
ENV PYTHONIOENCODING utf-8
RUN python3 -m pip install pipx
RUN python3 -m pipx ensurepath --force 
RUN . ~/.profile

# Install Lean
RUN curl https://raw.githubusercontent.com/leanprover/elan/master/elan-init.sh -sSf | sh -s -- -y 
ENV LEAN_PATH /root/.elan/toolchains/stable/lib/lean/library:/root/.lean/_target/deps/mathlib/src
ENV PATH=/root/.elan/bin:${PATH}
RUN pipx install mathlibtools
RUN /root/.local/bin/leanproject global-install

# That's it
#