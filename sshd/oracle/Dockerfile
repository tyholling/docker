FROM oraclelinux:8

RUN yum update -y \
&&  yum install -y \
openssh-server \
passwd \
;

RUN mkdir /var/run/sshd \
&&  passwd -d root \
&&  ssh-keygen -A \
;

COPY id_rsa.pub /root/.ssh/authorized_keys

EXPOSE 22

CMD [ "/usr/sbin/sshd", "-D" ]
