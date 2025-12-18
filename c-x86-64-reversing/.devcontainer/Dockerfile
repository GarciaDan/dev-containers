FROM mcr.microsoft.com/devcontainers/cpp:1-debian-12

# Install toolchain and reversing/analysis tools
RUN apt-get update && apt-get install -y \
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
 && rm -rf /var/lib/apt/lists/*

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