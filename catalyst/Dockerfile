# Should we pin to a specific ubuntu version to run this from?
# Should we even run ubuntu?
FROM ubuntu:jammy-20230605

# Should we pin to specific versions of ansible, packer and terraform?

ARG TERRAFORM_VERSION="1.5.0"
# This just does not work at all.
ARG ANSIBLE_VERSION="2.14.6-1ppa~jammy"
ARG PACKER_VERSION="1.9.1"

LABEL maintainer="Cuken <colin.uken@gmail.com>"
LABEL terraform_version=${TERRAFORM_VERSION}
LABEL ansible_version=${ANSIBLE_VERSION}
LABEL packer_version=${PACKER_VERSION}

ENV DEBIAN_FRONTEND=noninteractive
ENV TERRAFORM_VERSION=${TERRAFORM_VERSION}
ENV ANSIBLE_VERSION=${ANSIBLE_VERSION}
ENV PACKER_VERSION=${PACKER_VERSION}

RUN apt-get update \
    && apt-get install -y ansible curl python3 python3-pip python3-boto unzip


# https://releases.hashicorp.com/terraform/1.5.0/terraform_1.5.0_linux_amd64.zip

RUN curl -LO https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
    && curl -LO https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip \
    && unzip '*.zip' -d /usr/local/bin \
    && rm *.zip

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["/bin/bash"]
