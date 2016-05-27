FROM centos:centos7
MAINTAINER Chris O'Meara

ADD http://pkg.jenkins-ci.org/redhat/jenkins.repo /etc/yum.repos.d/jenkins.repo
RUN rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
RUN yum update -y && yum install -y wget initscripts java-1.8.0-openjdk jenkins && yum clean all

VOLUME /var/lib/jenkins
VOLUME /var/log/jenkins

# Expose Ports for web and slave agents
EXPOSE 8080
EXPOSE 50000

ENTRYPOINT [ "/usr/bin/java", "-DJENKINS_HOME=/var/lib/jenkins", "-jar", "/usr/lib/jenkins/jenkins.war", "--logfile=/var/log/jenkins/jenkins.log", "--webroot=/var/cache/jenkins/war" ]
