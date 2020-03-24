FROM centos:centos7

RUN yum update -y && \
    yum install -y openssh-server pwgen netcat net-tools curl wget && \
    yum clean all

RUN ssh-keygen -A

# Python and relevant tools
RUN yum update -y && yum groupinstall -y 'Development Tools' && \
    yum install -y python \
    libxml2-python \
    libxslt \
    zlib \
    libyaml \
    libffi \
    python-pip \
    pip

# Latest versions of python tools via pip 
#RUN pip install --upgrade pip && \ 
 #pip install virtualenv \ 
 #pip install requests

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN mkdir /root/.ssh
COPY id_rsa.pub /root/.ssh/authorized_keys
RUN chmod 400 /root/.ssh/authorized_keys

EXPOSE 22 
CMD ["/usr/sbin/sshd", "-D"]

 
