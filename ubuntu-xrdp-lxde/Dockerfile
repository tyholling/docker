FROM ubuntu

ENV DEBIAN_FRONTEND noninteractive

RUN apt update && apt upgrade && apt install --no-install-recommends --yes \
    lxde \
    supervisor \
    xorgxrdp \
    xrdp \
    xvfb \
;

RUN useradd --create-home --shell /bin/bash --user-group --groups sudo ubuntu
RUN echo "ubuntu:ubuntu" | chpasswd

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 3389

CMD ["/usr/bin/supervisord", "--nodaemon"]
