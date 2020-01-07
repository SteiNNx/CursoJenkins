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

COPY remote-key.pub /home/remote_user/.ssh/authorized_keys

RUN chown remote_user:remote_user -R /home/remote_user/.ssh && \
    chmod 600 /home/remote_user/.ssh/authorized_keys

run mkdir ~/.ssh && \
    chmod 700 -R ~/.ssh

RUN echo remote-key.pub >> ~/.ssh/authorized_keys && \
    chown -R remote_user:remote_user ~/.ssh && \
    chmod -R go= ~/.ssh

RUN rm -rf /run/nologin

CMD /usr/sbin/sshd -D
