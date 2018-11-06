#Dockerfile
 
FROM openjdk:8u151-jdk-alpine
 
RUN echo https://dl-3.alpinelinux.org/alpine/v3.6/main/ > /etc/apk/repositories
RUN echo https://dl-3.alpinelinux.org/alpine/v3.6/community/ >> /etc/apk/repositories
 
# Install packages
RUN apk add --no-cache bash build-base ca-certificates curl git openssh-client ttf-dejavu unzip docker python py-pip openssl sshpass python-dev openssl-dev libffi-dev openrc;
 
# Default to UTF-8 file.encoding
ENV LANG en_US.UTF-8
 
# Set the timezone
RUN set -eux; \
    apk add --no-cache --virtual .build-deps-tz tzdata; \
    cp /usr/share/zoneinfo/Asia/Singapore /etc/localtime; \
    echo "Asia/Singapore" > /etc/timezone; \
    apk del .build-deps-tz
 
# Create the jenkins user
#RUN addgroup -g ${gid} ${group} && \
#    adduser -u ${uid} -G ${group} -s /bin/sh -D ${user}
 
#WORKDIR /home/${user}
 
# Set JENKINS_HOME
#ENV JENKINS_HOME /var/jenkins_home
#RUN mkdir "${JENKINS_HOME}" && chown -R ${user}:${group} "${JENKINS_HOME}"
 
# Install ruby fpm
RUN set -eux; \
    apk add --no-cache libffi-dev rpm ruby ruby-dev ruby-irb ruby-rdoc; \
    chmod 1777 /var/tmp; \
    gem install fpm
 
# Install maven
ENV MAVEN_HOME /usr/share/java/maven-3
 
RUN apk add --no-cache maven
 
# Install Postgres Client
RUN apk add --no-cache postgresql-client
  
# Install ansible
#ENV ANSIBLE_VERSION 2.5.2
 
#RUN set -eux; \
#    apk add --no-cache python py-pip openssl sshpass ; \
#    apk add --no-cache --virtual .build-deps python-dev openssl-dev libffi-dev; \
#    pip install --upgrade pip cffi; \
#               pip install netaddr; \
#    pip install ansible==${ANSIBLE_VERSION}; \
#    pip install --upgrade pywinrm; \
#    apk del .build-deps


RUN pip install jenkins-webapi

#RUN easy_install jenkins-webapi

RUN rc-update add docker boot

RUN curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker$
RUN mkdir -p /home/jenkins
RUN mkdir -p /var/lib/jenkins

ADD slave.py /var/lib/jenkins/slave.py

WORKDIR /home/jenkins

ENV JENKINS_URL "http://jenkins"
ENV JENKINS_SLAVE_ADDRESS ""
ENV JENKINS_USER "admin"
ENV JENKINS_PASS "admin"
ENV SLAVE_NAME ""
ENV SLAVE_SECRET ""
ENV SLAVE_EXECUTORS "1"
ENV SLAVE_LABELS "java maven"
ENV SLAVE_WORING_DIR ""
ENV CLEAN_WORKING_DIR "true"

CMD [ "python", "-u", "/var/lib/jenkins/slave.py" ]

#--------------------------------------------------------------------------------------------------------------------
# Install packer
#ENV PACKER_VERSION 1.2.3
 
#RUN set -eux; \
#    curl -kSLO --compressed "https://10.138.151.57/pub/dist/hashicorp/packer_${PACKER_VERSION}_linux_amd64.zip"; \
#    unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /usr/local/bin; \
#    rm -f packer_${PACKER_VERSION}_linux_amd64.zip
 
# Install terraform
#ENV TERRAFORM_VERSION 0.11.7
 
#RUN set -eux; \
#    curl -kSLO --compressed "https://10.138.151.57/pub/dist/hashicorp/terraform_${TERRAFORM_VERSION}_linux_amd64.zip"; \
#    unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /usr/local/bin; \
#    rm -f terraform_${TERRAFORM_VERSION}_linux_amd64.zip
 
# Install jenkins swarm client
#RUN set -eux; \
#    mkdir -p /usr/share/java; \
#    curl -kSL "https://10.138.151.57/pub/dist/jenkins/swarm-client-3.12.jar" -o /usr/share/java/swarm-client.jar
 
#RUN chown -R ${user}:${group} /home/${user}
 
# Switch to the jenkins user
#USER ${user}
#RUN git config --global http.sslVerify false
#COPY jenkins-slave.sh /usr/local/bin/jenkins-slave.sh
#ENTRYPOINT ["/usr/local/bin/jenkins-slave.sh"] 
#Jenkins-salve.sh
 
 

