FROM debian:bullseye

ARG DEBIAN_FRONTEND=noninteractive
ARG USER_UID=1000
ARG USER_GID=1000
ARG USERNAME=bullseye

#RUN echo 'Acquire::http::Proxy "http://192.168.0.9:3142";' > /etc/apt/apt.conf.d/01proxy
RUN sed -i 's/ main / main contrib non-free non-free-firmware/' /etc/apt/sources.list
RUN echo "deb http://archive.debian.org/debian bullseye-backports main contrib non-free" > /etc/apt/sources.list.d/bullseye-backports.list
RUN apt-get update 
RUN apt-get install -y \
    apt-utils \
    bison \
    build-essential \
    bzip2 \
    ca-certificates \
    ccache \
    check \
    curl \
    cmake-latest \
    flex \
    git \
    git-lfs \
    gperf \
    lcov \
    libbsd-dev \
    libffi-dev \
    libglib2.0-0 \
    libncurses-dev \
    libpixman-1-0 \
    libsdl2-2.0-0 \
    libslirp0 \
    libusb-1.0-0-dev \
    make \
    ninja-build \
    python3 \
    python3-venv \
    python3-crcmod \
    ruby \
    sudo \
    unzip \
    usbutils \
    wget \
    xz-utils \
    zip \
    build-essential pkg-config yasm \
    libsqlite3-dev \
    libxv-dev libvdpau-dev libva-dev libglu1-mesa-dev \
    libasound2-dev libpulse-dev \
    libx264-dev libxvidcore-dev \
    libmp3lame-dev libtwolame-dev libopus-dev libvorbis-dev libogg-dev \
    libpng-dev libass-dev \
    file \
    squashfs-tools 
    # app image
  RUN apt-get install -y  desktop-file-utils fakeroot fuse  patchelf python3-pip python3-setuptools squashfs-tools strace util-linux zsync 
  RUN apt-get install -y  zsh neovim

  RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 10 \
  && :
    #libaften-dev \

RUN useradd -m bullseye && usermod --shell /usr/bin/zsh bullseye
RUN chmod a+rwx /opt /usr/local/bin
#
#

# 
# 
# 
# Extra packages
# 
# 
# 

    #libfaac-dev \
    #libfdk-aac-dev \
#libfuse2t64

# 
CMD [ "/bin/bash" ]

# install golang
RUN cd /tmp && wget https://go.dev/dl/go1.23.6.linux-amd64.tar.gz && tar -C /usr/local -xzf go1.23.6.linux-amd64.tar.gz

# Add to PATH (add this to ~/.bashrc or ~/.zshrc)

###################################
# Setup user env
###################################
USER ${USERNAME}
RUN mkdir ~/.local &&  mkdir ~/.local/bin &&  mkdir ~/.cargo && mkdir ~/.cargo/bin
#
RUN cat <<EOF > /home/bullseye/.zshrc
# History Settings
HISTFILE=~/.zsh_history
HISTSIZE=10000
SAVEHIST=10000
setopt appendhistory
setopt sharehistory

# Completion System
autoload -Uz compinit && compinit

# Prompt
PROMPT='%F{cyan}[%n@docker]%f %F{blue}%~%f %# '

# Aliases
alias ls='ls --color=auto'
alias ll='ls -lah'
EOF
# give access to image tool
ENV PATH="/usr/local/go/bin/:$PATH"



