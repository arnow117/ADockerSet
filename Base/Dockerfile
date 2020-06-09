FROM ubuntu:18.04

MAINTAINER arnow117 "arnow117@gmail.com"


RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y git vim curl wget python python3 python-pip python3-pip tmux openssh-server sudo net-tools libunwind8 binutils-dev pkg-config make cmake libssl-dev iputils-ping iproute2 libunwind-dev
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install ntp tzdata
RUN echo "install essential basic apps"

RUN useradd -d /home/arnow117 -m arnow117 && echo "arnow117:123456" | chpasswd && adduser arnow117 sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
WORKDIR /home/arnow117
USER arnow117
ENV TOOLS_PATH /home/arnow117/tools
ENV WORK_PATH /home/arnow117/workspace
ENV SCRIPT_PATH /home/arnow117/scripts
RUN mkdir $TOOLS_PATH $WORK_PATH $SCRIPT_PATH
#Config awesome vim
RUN git clone --depth=1 git://github.com/amix/vimrc.git ~/.vim_runtime
RUN sh ~/.vim_runtime/install_basic_vimrc.sh

#Install&config oh-my-zsh
RUN sudo apt-get install -y zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh


#Config PIP for China & install IPython
RUN mkdir -p /home/arnow117/.config/pip
COPY pip.conf /home/arnow117/.config/pip/pip.conf
RUN pip3 install ipython
RUN sudo chsh -s /usr/bin/zsh arnow117

#install rust&config
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
RUN mkdir -p /home/arnow117/.cargo
COPY rust.config /home/arnow117/.cargo/config
#change to nightly
RUN . ~/.cargo/env; rustup default nightly; rustup update

# install go&config
ENV GO_ARCHIVE=go1.14.4.linux-amd64.tar.gz
RUN wget https://dl.google.com/go/$GO_ARCHIVE
RUN sudo tar -C /usr/local -xzf $GO_ARCHIVE; rm -rf $GO_ARCHIVE
RUN mkdir -p ~/go_dep

# fzf
RUN git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
# mv zshrc here for better cache
COPY zshrc /home/arnow117/.zshrc
RUN sudo ~/.fzf/install --all

#start sshd
RUN sudo mkdir /var/run/sshd
CMD ["sudo","/usr/sbin/sshd","-D"]

WORKDIR $WORK_PATH
