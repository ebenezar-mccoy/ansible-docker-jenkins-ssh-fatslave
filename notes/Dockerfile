# docker jenkis slave base
FROM jenkins/ssh-slave

# ansible tools
RUN apt-get update \
  && apt-get install -y python3-pip \
  && apt-get autoremove -y && apt-get autoclean -y && apt-get clean -y \
  && pip3 install ansible
