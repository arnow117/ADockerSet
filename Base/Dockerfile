FROM ubuntu:18.04

MAINTAINER arnow117 "arnow117@gmail.com"


RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y git vim curl wget python python3 python-pip python3-pip tmux openssh-server sudo net-tools libunwind8 binutils-dev
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install ntp tzdata
RUN echo "install essential basic apps"

RUN useradd -d /home/arnow117 -m arnow117 && echo "arnow117:arnow117" | chpasswd && adduser arnow117 sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
WORKDIR /home/arnow117
USER arnow117
ENV TOOLS_PATH /home/arnow117/Tools
ENV WORK_PATH /home/arnow117/Workspace
RUN mkdir $TOOLS_PATH $WORK_PATH
#Config awesome vim
RUN git clone --depth=1 git://github.com/amix/vimrc.git ~/.vim_runtime
RUN sh ~/.vim_runtime/install_basic_vimrc.sh

#Install&config oh-my-zsh
RUN sudo apt-get install -y zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
RUN sudo chsh -s /bin/zsh
COPY zshrc /home/arnow117/.zshrc

#Config PIP for China & install IPython
RUN mkdir -p /home/arnow117/.config/pip
COPY pip.conf /home/arnow117/.config/pip/pip.conf
RUN pip3 install ipython

# ENV DEBIAN_FRONTEND=noninteractive 
# ENV TZ=Asia/Shanghai
# RUN sudo ln -snf /usr/share/zoneinfo/$TZ /etc/localtime 
# RUN sudo touch /etc/timezone
# RUN sudo echo "$TZ" > /etc/timezone

#install tzdata package
# RUN sudo apt-get install -y ntp tzdata
# set your timezone
# RUN sudo ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
# RUN sudo dpkg-reconfigure --frontend noninteractive tzdata

WORKDIR $WORK_PATH

