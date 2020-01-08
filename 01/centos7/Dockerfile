FROM centos

#Instalo openssh
RUN yum update -y

RUN yum -y install openssh-clients && \
    yum -y install openssh-server sudo && \
    yum -y install passwd


#Agrego usuario
RUN useradd remote_user -G root && \
    echo "1234" | passwd remote_user --stdin && \
    mkdir /home/remote_user/.ssh && \
    chmod 700 -R /home/remote_user/.ssh

RUN echo '%root ALL=(ALL) ALL' >> /etc/sudoers

COPY remote-key.pub /home/remote_user/.ssh/authorized_keys

RUN chown remote_user:remote_user -R /home/remote_user && \
    chmod 600 /home/remote_user/.ssh/authorized_keys

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N '' 

RUN yum -y install mysql
RUN yum -y install epel-release  
RUN yum -y install python3-pip && \
    pip3 install --upgrade pip

RUN pip3 install awscli

CMD /usr/sbin/sshd -D