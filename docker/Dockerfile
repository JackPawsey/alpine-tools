FROM alpine:3.18.4

ENV TERRAFORM_VERSION=1.5.7
ENV ANSIBLE_HOST_KEY_CHECKING=False

RUN apk -U upgrade \
  && apk add openssl openssh-client curl tar gzip unzip bash ca-certificates git jq ncurses python3 py3-botocore py3-boto3 ansible aws-cli

# Ansible setup
RUN mkdir -p etc/ansible/hosts
COPY ./ansible-dynamic-inventory/ec2.py etc/ansible/hosts/
RUN chmod +x etc/ansible/hosts/ec2.py

# install Terraform
RUN curl -O https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
  && unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
  && rm terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
  && mv terraform /usr/local/bin
