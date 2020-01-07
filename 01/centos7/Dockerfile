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
RUN yum -y install python36 python3-virtualenv

RUN python3.6 -m virtualenv --python=python3.6 env && \
    ./env/bin/python3.6 -m pip install -U pip 

#RUN ./env/bin/python3.6 -m pip download --only-binary :all: --platform macosx_10_10_intel --python-version 27 --abi cp27 -v numpy==1.16.0

#ENV pip = lib/python3.6/site-packages/pip/index.py

#RUN pip install awscli


CMD /usr/sbin/sshd -D