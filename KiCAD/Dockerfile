FROM fedora:22
MAINTAINER Marcel Beltz <marcel@beltz.info>

RUN dnf -y update && dnf clean all
RUN dnf -y install dnf-plugins-core sudo
RUN dnf -y copr enable mangelajo/kicad
RUN dnf -y install kicad
RUN dnf clean all
RUN export uid=501 gid=501 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer

USER developer
ENV HOME /home/developer
CMD /usr/bin/kicad
