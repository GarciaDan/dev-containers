FROM mcr.microsoft.com/devcontainers/cpp:1-debian-12

# Install toolchain and reversing/analysis tools
RUN apt-get update && apt-get install -y \
    curl \
    build-essential \
    gdb \
    lldb \
    cmake \
    ninja-build \
    pkg-config \
    clang \
    clang-format \
    clang-tidy \
    valgrind \
    binutils \
    gcc-multilib \
    ssh \
    openssh-server \
    nasm \
    meson \
    checksec \
    jq 

 # Install radare2
RUN LATEST_VERSION=$(curl -s https://api.github.com/repos/radareorg/radare2/releases/latest | jq -r '.tag_name') && \
    curl -Ls "https://github.com/radareorg/radare2/releases/download/${LATEST_VERSION}/radare2-${LATEST_VERSION}.tar.xz" | tar xJv && \
    ./radare2-${LATEST_VERSION}/sys/install.sh && \
    rm -rf /var/lib/apt/lists/*

 # Directory for SSH
RUN mkdir -p /var/run/sshd  
  
# VSCode password
RUN echo 'vscode:vscode' | chpasswd  
  
# Allow login using password
RUN sed -i 's/^#\?PasswordAuthentication .*/PasswordAuthentication yes/' /etc/ssh/sshd_config \  
 && sed -i 's/^#\?PermitRootLogin .*/PermitRootLogin no/' /etc/ssh/sshd_config  
  
# Expose port 22 in container
EXPOSE 22

# Set workspace
WORKDIR /workspace