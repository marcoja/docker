FROM centos:7
MAINTAINER Marco Jasso <mjasso@itexico.net>

#Update base os
RUN yum makecache
RUN yum update -y

#Util packages
RUN yum install -y which
RUN yum install -y wget
RUN yum install -y curl
RUN yum install -y zip unzip
RUN yum install -y openssh-clients
RUN yum clean all

#Global variables
ENV JENKINS_HOME /var/jenkins_home
ENV TINI_VERSION v0.13.2

#setup tini as a subreaper
#https://github.com/krallin/tini/issues/8
#https://github.com/krallin/tini
#RUN curl -fL https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini-static -o /bin/tini
#RUN chmod +x /bin/tini

#create jenkins user
RUN useradd -c "Jenkins default user" -d "$JENKINS_HOME" -u 1000 -m -s /bin/bash jenkins

#create a volume (mountedmon data container)
VOLUME /var/jenkins_home


#copy ssh keys
USER jenkins
RUN umask 022
RUN mkdir /var/jenkins_home/.ssh
USER root
COPY id_rsa /var/jenkins_home/.ssh/id_rsa
COPY id_rsa.pub /var/jenkins_home/.ssh/id_rsa.pub
RUN chown -R jenkins:jenkins /var/jenkins_home/.ssh/
RUN chown -R jenkins:jenkins /var/jenkins_home/.ssh/id_rsa
RUN chown -R jenkins:jenkins /var/jenkins_home/.ssh/id_rsa.pub

#ENTRYPOINT ["/bin/tini", "--", "/usr/local/bin/jenkins.sh"]
#ENTRYPOINT ["/bin/tini"]
