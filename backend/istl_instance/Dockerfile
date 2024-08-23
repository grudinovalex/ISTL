FROM fedora:latest

LABEL maintainer="grudinov.alex@gmail.com"

SHELL ["/bin/bash", "-c"]

RUN sed -i '/tsflags=nodocs/d' /etc/dnf/dnf.conf && \
    yum update -y && \
    yum upgrade -y && \
    rpm -qa | sort | sed 's/-[0-9].*[0-9]*//g' | xargs dnf -y reinstall && \
    yum update -y && \
    yum upgrade -y && \
    yum install -y man-pages man-db man ncurses vim groff cowsay htop iputils wget git tree nano binutils bind-utils file cmatrix iproute procps unzip sshpass nano pcre2-tools openssh-server cracklib-dicts && \
    mandb && \
    dnf update && \
    echo 'istl2024' | passwd --stdin root && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N '' && \
    adduser trainee && \
    echo 'istl2024' | passwd --stdin trainee && \
    usermod -aG wheel trainee && \
    mkdir /mnt/host


COPY my_banner_message /etc/motd.d
COPY --chown=trainee:trainee trainee_home/chapter_1 /home/trainee/chapter_1
COPY --chown=trainee:trainee trainee_home/chapter_2 /home/trainee/chapter_2
COPY --chown=trainee:trainee trainee_home/chapter_3 /home/trainee/chapter_3
COPY --chown=trainee:trainee trainee_home/chapter_4 /home/trainee/chapter_4
COPY --chown=trainee:trainee trainee_home/chapter_5 /home/trainee/chapter_5
COPY trainee_home/.vimrc /home/trainee

COPY usr_local_bin/ch* /usr/local/bin
COPY --chown=trainee:trainee usr_local_bin/files /usr/local/bin/files

COPY --chown=trainee:trainee mnt_host/chapter_1_orig /mnt/host/chapter_1_orig
COPY --chown=trainee:trainee mnt_host/chapter_2_orig /mnt/host/chapter_2_orig
COPY --chown=trainee:trainee mnt_host/chapter_3_orig /mnt/host/chapter_3_orig

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
