FROM centos:centos7
MAINTAINER Chris O'Meara

ADD http://pkg.jenkins-ci.org/redhat/jenkins.repo /etc/yum.repos.d/jenkins.repo
RUN rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
COPY docker.repo /etc/yum.repos.d/docker.repo
RUN yum update -y && yum install -y wget initscripts java-1.8.0-openjdk-devel jenkins ssh git unzip docker-engine-1.9.1-1.el7.centos sudo && yum clean all

## Allow jenkins to run in-container commands as root
COPY sudoers /etc/sudoers
COPY sudoers.d/99_jenkins /etc/sudoers.d/99_jenkins

## Helper scripts
COPY parent-portal-ecs-task /opt/parent-portal-build-help/parent-portal-ecs-task
RUN chmod +x /opt/parent-portal-build-help/parent-portal-ecs-task
COPY parent-portal-ecs-task.json.erb /opt/parent-portal-build-help/parent-portal-ecs-task.json.erb

## Install AWS CLI
RUN cd /tmp && wget -q https://s3.amazonaws.com/aws-cli/awscli-bundle.zip && unzip awscli-bundle.zip && awscli-bundle/install -i /opt/aws

## Deploy the run script, can't put it in /var/lib/jenkins because that volume will be mounted from Docker
COPY run /jenkins
RUN chmod +x /jenkins

VOLUME /var/lib/jenkins
VOLUME /var/log/jenkins

## Expose Ports for web and slave agents
EXPOSE 8080
EXPOSE 50000

USER jenkins

ENTRYPOINT [ "/jenkins" ]
