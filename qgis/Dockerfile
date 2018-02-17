#
# QGIS nightly
#
# docker run --rm -d \
#   -v /tmp/.X11-unix/:/tmp/.X11-unix \
#   -e DISPLAY=$DISPLAY \
#   -v ~/.Xauthority:/tmp/.Xauthority:ro \
#   -e XAUTHORITY=/tmp/.Xauthority \
#   -h $(hostname) \
#   --name qgis \
#   qgis
#
FROM debian:stretch

LABEL maintainer "Tilman Dilo <tilman.dilo@gmail.com>"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y \
	gnupg

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-key CAEB3DC3BDF7FB45

RUN echo "deb http://qgis.org/debian-nightly stretch main" >> /etc/apt/sources.list.d/qgis.list

RUN apt-get update && apt-get install -y --no-install-recommends \
	qgis \
	python-qgis \
	qgis-plugin-grass \
	&& rm -rf /var/lib/apt/lists/*

ENV HOME /home/qgis
RUN useradd --create-home --home-dir $HOME qgis

WORKDIR $HOME
USER qgis

ENV QT_X11_NO_MITSHM 1

CMD qgis --version-migration
