FROM centos:centos7
MAINTAINER Chris O'Meara

ADD http://pkg.jenkins-ci.org/redhat/jenkins.repo /etc/yum.repos.d/jenkins.repo
RUN rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
COPY docker.repo /etc/yum.repos.d/docker.repo
RUN yum update -y && yum install -y wget initscripts java-1.8.0-openjdk jenkins ssh git unzip docker-engine sudo && yum clean all

## Allow jenkins to run in-container commands as root
COPY sudoers /etc/sudoers
COPY sudoers.d/99_jenkins /etc/sudoers.d/99_jenkins

## Install AWS CLI
RUN cd /tmp && wget -q https://s3.amazonaws.com/aws-cli/awscli-bundle.zip && unzip awscli-bundle.zip && awscli-bundle/install -i /opt/aws

## Deploy SSH keys and config
COPY .ssh/* /var/lib/jenkins/.ssh/
RUN chmod 700 /var/lib/jenkins/.ssh

## Deploy the run script
COPY run /var/lib/jenkins/run
RUN chmod +x /var/lib/jenkins/run

VOLUME /var/lib/jenkins
VOLUME /var/log/jenkins

## Expose Ports for web and slave agents
EXPOSE 8080
EXPOSE 50000

USER jenkins

ENTRYPOINT [ "/var/lib/jenkins/run" ]
