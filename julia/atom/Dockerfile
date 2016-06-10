# docker run -it \
# -v /tmp/.X11-unix:/tmp/.X11-unix \ # mount the X11 socket
# -e DISPLAY=unix$DISPLAY \ # pass the display
# --device /dev/snd \ # so we have sound
# --name atom \
# -p 9090:8888 -v /mnt/LinuxData/ceshine/:/data \
# julia-atom

FROM julia:latest

ENV ATOM_VERSION v1.7.3

RUN apt-get update && \
    apt-get install -y git \
                       curl \
                       ca-certificates \
                       libgtk2.0-0 \
                       libxtst6 \
                       libnss3 \
                       libgconf-2-4 \
                       libasound2 \
                       fakeroot \
                       gconf2 \
                       gconf-service \
                       libcap2 \
                       libnotify4 \
                       libxtst6 \
                       libnss3 \
                       gvfs-bin \
                       cmake \
                       xdg-utils && \
    apt-get clean

RUN curl -L https://github.com/atom/atom/releases/download/${ATOM_VERSION}/atom-amd64.deb > /tmp/atom.deb && \
    dpkg -i /tmp/atom.deb && \
    rm -f /tmp/atom.deb && \
    useradd -d /home/atom -m atom

USER atom

CMD ["/usr/bin/atom","-f"]
