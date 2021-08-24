FROM devopsfaith/krakend

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    gnupg2 \
    lsb-release \
    software-properties-common \
    dnsutils \
    iputils-ping

RUN curl -fsSL https://apt.releases.hashicorp.com/gpg | apt-key add -
RUN apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
RUN apt-get update && apt-get install consul

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN mkdir /tmp/consul
COPY ./krakend-service.json /etc/consul.d/krakend-service.json

WORKDIR /etc/consul.d

# Nao esquecer que precisa colcoar o web.json dentro dos containers para subir o servico. dentro do diretorio /etc/consul.d
# consul agent -server -ui -client 0.0.0.0 -bootstrap-expect=1 -node=master -data-dir=/tmp/consul -config-dir=/etc/consul.d
# consul agent -node=s1 -enable-local-script-checks=true -data-dir=/tmp/consul -config-dir=/etc/consul.d
# consul agent -node=s2 -enable-local-script-checks=true -data-dir=/tmp/consul -config-dir=/etc/consul.d
# consul agent -join=master -enable-local-script-checks=true -data-dir=/tmp/consul -config-dir=/etc/consul.d

# dig @localhost -p 8600 webserver.service.dc1.consul. A
# dig @master -p 53 webserver.service.dc1.consul. A
