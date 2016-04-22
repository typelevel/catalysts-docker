FROM centos:centos7

MAINTAINER InTheNow

LABEL Add Artifactory repositories
ADD ["Artifactory-oss.repo","/etc/yum.repos.d/"]

RUN yum -y update; yum clean all
RUN yum install  java-1.8.0-openjdk-devel rsync net-tools  -y && \
yum clean all

LABEL Install Artifactory

EXPOSE 8081

ADD runArtifactory.sh /tmp/run.sh
RUN chmod +x /tmp/run.sh && \
    yum install -y --enablerepo="Artifactory-oss" jfrog-artifactory-oss

LABEL Create Folders that aren't exists, and make sure they are owned by Artifactory, \
Without this action, Artifactory will not be able to write to external mounts
RUN mkdir -p /etc/opt/jfrog/artifactory /var/opt/jfrog/artifactory/{data,logs,backup} && \
    chown -R artifactory: /etc/opt/jfrog/artifactory /var/opt/jfrog/artifactory/{data,logs,backup} && \
    mkdir -p /var/opt/jfrog/artifactory/defaults/etc && \
    cp -rp /etc/opt/jfrog/artifactory/* /var/opt/jfrog/artifactory/defaults/etc/
ENV ARTIFACTORY_HOME /var/opt/jfrog/artifactory

LABEL Add default configuration containing repositories
ADD artifactory/artifactory.config.xml /etc/opt/jfrog/artifactory/artifactory.config.xml

CMD /tmp/run.sh
