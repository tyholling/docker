FROM ubuntu

RUN apt update && apt install --no-install-recommends --yes \
openssh-server \
;

RUN mkdir /var/run/sshd
COPY id_rsa.pub /root/.ssh/authorized_keys

EXPOSE 22
CMD [ "/usr/sbin/sshd", "-D" ]
