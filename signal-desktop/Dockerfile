#
# Signal Desktop
#
# docker run --rm -d \
#   -v /tmp/.X11-unix/:/tmp/.X11-unix \
#   -e DISPLAY=$DISPLAY \
#   -v ~/.Xauthority:/tmp/.Xauthority:ro \
#   -e XAUTHORITY=/tmp/.Xauthority \
#   -h $(hostname) \
#   --name signal \
#   signal
#
FROM debian:stretch

LABEL maintainer "Tilman Dilo <tilman.dilo@gmail.com>"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
	ca-certificates \
	apt-transport-https \
	curl \
	gnupg

RUN curl -o /tmp/keys.asc https://updates.signal.org/desktop/apt/keys.asc
RUN apt-key add /tmp/keys.asc
RUN echo "deb [arch=amd64] https://updates.signal.org/desktop/apt xenial main" | tee -a /etc/apt/sources.list.d/signal-xenial.list

RUN apt-get update && apt-get install -y \
	signal-desktop

ENV HOME /home/signal
RUN useradd --create-home --home-dir $HOME signal

WORKDIR $HOME
USER signal

CMD signal-desktop
