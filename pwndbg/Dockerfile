FROM ubuntu:18.04

# adding i386 architecture
RUN dpkg --add-architecture i386

# upgrading the image
RUN apt-get update
RUN apt-get --assume-yes dist-upgrade

# install various required tools
RUN apt-get --assume-yes install man locales tmux
RUN apt-get --assume-yes install socat \
			build-essential libc6:i386 libncurses5:i386\
			libstdc++6:i386 gdb git strace ltrace

# install pwndbg
RUN git clone https://github.com/pwndbg/pwndbg /opt/pwndbg
RUN cd /opt/pwndbg; ./setup.sh

# install pwntools
RUN pip install --upgrade pip
RUN pip install --upgrade pwntools

# setup locale
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

# cleanup
RUN rm -rf /var/lib/apt/lists/*
RUN rm -rf /root/.cache
RUN rm -rf /var/lib/apt/archives/*