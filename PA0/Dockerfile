# setting base image
FROM debian

RUN apt-get update

 # Set the locale
RUN apt-get install -y locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen
RUN dpkg-reconfigure --frontend=noninteractive locales
RUN update-locale LANG=en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

 # new a directory for sshd to run
RUN mkdir -p /var/run/sshd
 # installing ssh server
RUN apt-get install -y openssh-server

 # installing sudo
RUN apt-get install -y sudo

 # make ssh services use IPv4 to let X11 forwarding work correctly
RUN echo AddressFamily inet >> /etc/ssh/sshd_config

 # defining user account imformation
ARG username=ics
ARG userpasswd=ics

 # adding user
RUN useradd -ms /bin/bash $username && (echo $username:$userpasswd | chpasswd)

 # adding user to sudo group
RUN adduser $username sudo

 # setting running application
CMD /usr/sbin/sshd -D