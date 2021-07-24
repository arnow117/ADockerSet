FROM ubuntu:18.04

MAINTAINER arnow117 "arnow117@gmail.com"

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y git vim curl wget tmux openssh-server sudo net-tools libunwind8 binutils-dev pkg-config build-essential make cmake autotools-dev autoconf libtool iputils-ping iproute2 htop 
# for sth dev
RUN apt-get install -y python python3 python-pip python3-pip clang libclang-dev libssl-dev libunwind-dev gcc-7-plugin-dev
# install m32 support
RUN apt-get install -y gcc-multilib
# ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# set no interactive apt install
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install ntp tzdata
RUN echo "install essential basic apps"
# add user & empty sudo pass
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
RUN sudo chsh -s /usr/bin/zsh arnow117

#Config PIP for China & install IPython
RUN mkdir -p /home/arnow117/.config/pip
COPY --chown=arnow117:arnow117 pip.conf /home/arnow117/.config/pip/pip.conf
RUN pip3 install -U ipython

#install rust&config
ENV RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static
ENV RUSTUP_UPDATE_ROOT=https://mirrors.ustc.edu.cn/rust-static/rustup
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
RUN mkdir -p /home/arnow117/.cargo
COPY --chown=arnow117:arnow117 rust.config /home/arnow117/.cargo/config
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
COPY --chown=arnow117:arnow117 zshrc /home/arnow117/.zshrc
RUN sudo ~/.fzf/install --all

#config sshd
RUN sudo mkdir /var/run/sshd
RUN sudo sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
EXPOSE 22/tcp
#start sshd
CMD ["sudo","/usr/sbin/sshd","-D"]

WORKDIR $WORK_PATH
