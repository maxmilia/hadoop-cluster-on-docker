FROM ubuntu:bionic

RUN apt-get update && \
    apt-get install -yqq  openssh-client openssh-server

RUN echo 'root:root' |chpasswd

RUN mkdir /var/run/sshd

RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN mkdir /root/.ssh

COPY ./ssh/id_rsa.pub /root/.ssh/id_rsa.pub

RUN cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys

RUN chmod 700 -R /root/.ssh

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]