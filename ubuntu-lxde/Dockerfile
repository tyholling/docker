FROM ubuntu

ENV DEBIAN_FRONTEND noninteractive

RUN apt update --yes \
&&  apt install --yes \
    supervisor \
    openssh-server \
;

RUN useradd --create-home --shell /bin/bash --user-group --groups sudo ubuntu
RUN echo "ubuntu:ubuntu" | chpasswd

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 22
CMD ["/usr/bin/supervisord", "--nodaemon"]
