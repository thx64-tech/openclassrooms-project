FROM ubuntu:latest
ARG ssh_pass=poiuytre
RUN \ 
  apt update &&\
  apt install -y openssh-server openssl &&\
  mkdir /var/run/sshd &&\
  sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config &&\
  sed -i "s/SSH_PORT/$SSH_PORT/g" /etc/ssh/sshd_config &&\
  useradd -rm -d /home/aic -p $(openssl passwd -1 $ssh_pass) -s /bin/bash -g root -G sudo -u 1000 aic  &&\
  usermod -g www-data aic && usermod -aG www-data,root root &&\
  echo 'root:root' | chpasswd &&\
  service ssh start 

ADD . /app
ADD ./app/ssh/sshd_config /etc/ssh/sshd_config
WORKDIR /
EXPOSE 22 
CMD ["/usr/sbin/sshd","-D"]
