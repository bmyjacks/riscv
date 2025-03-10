FROM debian:bookworm

RUN apt update
# Install and Configure SSH
RUN apt install -y openssh-server
RUN echo 'root:riscv' | chpasswd # set password to 'riscv'
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN mkdir /var/run/sshd
RUN chmod 0755 /var/run/sshd

# Install vim nano
RUN apt install -y vim nano

# Install QEMU
RUN apt install -y qemu-user-static

# Install gcc
RUN apt install -y gcc-riscv64-linux-gnu g++-riscv64-linux-gnu
RUN cp /usr/riscv64-linux-gnu/lib/ld-linux-riscv64-lp64d.so.1 /lib/ld-linux-riscv64-lp64d.so.1

# Add PATH and LD_LIBRARY_PATH
RUN echo "export PATH=$PATH:/usr/bin" >>/root/.bash_profile
RUN echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/riscv64-linux-gnu/lib:/usr/lib/aarch64-linux-gnu" >>/root/.bash_profile

WORKDIR /root
COPY cplusplus.cpp /root/cplusplus.cpp

EXPOSE 22

# Start SSH server
CMD ["/usr/sbin/sshd", "-D"]
