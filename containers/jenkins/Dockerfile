FROM jenkins/jenkins:latest
MAINTAINER febef (febef.dev@gmail.com)
USER root

RUN apt-get update && apt-get install -y tree nano curl sudo ; \
    curl https://get.docker.com/builds/Linux/x86_64/docker-latest.tgz | tar xvz -C /tmp/ && mv /tmp/docker/docker /usr/bin/docker ; \
    curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose ; \
    chmod 755 /usr/local/bin/docker-compose ; \
    apt-get clean --dry-run; \
    usermod -a -G sudo jenkins ; \
    echo "jenkins ALL=(ALL:ALL) NOPASSWD:ALL" >> /etc/sudoers ;

ENV CASC_JENKINS_CONFIG="/tmp/jenkins.yml"
COPY jenkins.yml ${CASC_JENKINS_CONFIG}

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

FROM jenkins/jenkins:latest

RUN /usr/local/bin/install-plugins.sh git matrix-auth workflow-aggregator docker-workflow blueocean credentials-binding

ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

USER jenkins
