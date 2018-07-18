FROM python:3.6

ARG TERRAFORM_VERSION=0.10.8

ENV DEBIAN_FRONTEND=noninteractive \
    GHE_USEREMAIL=MAIL \
    GHE_USERNAME=NAME \
    LANG=C.UTF-8

RUN echo "deb http://debian-mirror.sakura.ne.jp/debian/ jessie main contrib non-free" > /etc/apt/sources.list
RUN apt-get clean && \
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/* && \
    apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y --no-install-recommends unzip git zip jq ca-certificates curl lsb-release gawk

# configure timezone
RUN echo "Asia/Tokyo" > /etc/timezone
RUN  dpkg-reconfigure -f noninteractive tzdata

# install Terraform
RUN mkdir /tmp/terraform
RUN cd /tmp/terraform
RUN curl -O -sS -L https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip
RUN unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip
RUN rm terraform_${TERRAFORM_VERSION}_linux_amd64.zip
RUN mv terraform* /usr/local/bin
RUN rm -rf /tmp/terraform

# install python modules
RUN pip install pyaml
RUN pip install boto3

#RUN git config --global user.email ${GHE_USEREMAIL} && \
#    git config --global user.name ${GHE_USERNAME}

RUN apt-get clean
RUN rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
