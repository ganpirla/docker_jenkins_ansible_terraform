FROM jenkins/jenkins

USER root

RUN apt-get update && apt-get install python3-pip wget -y && \
    pip3 install ansible --upgrade

ENV TERRAFORM_VERSION=1.3.6

RUN wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /usr/bin

USER jenkins
