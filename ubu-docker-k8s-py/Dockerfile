#FROM ubuntu:16.04

#curl -fsSL get.docker.com -o get-docker.sh
#RUN apt-get update
#RUN apt-get update && apt-get install -y \
    #curl
#RUN curl -sSL https://get.docker.com | sh

#CMD ["echo", "hello-world"]


FROM golang:1.10-stretch

COPY kube /home/kube/
COPY minikube /home/minikube/
#RUN cat /home/kube/config && ls /home/minikube/

ENV DOCKER_CHANNEL=stable \
    DOCKER_VERSION=18.03.1-ce

# Install Docker, Docker Compose, Docker Squash
RUN apt-get update && apt-get install -y \
    curl \
    python-pip \
    libdevmapper-dev \
    iptables \
    ca-certificates \
    && \
    curl -fL "https://download.docker.com/linux/static/${DOCKER_CHANNEL}/x86_64/docker-${DOCKER_VERSION}.tgz" | tar zx && \
    mv docker/* /bin/ && chmod +x /bin/docker* && \
    rm -rf /var/cache/apt/* && \
    rm -rf /root/.cache

RUN curl -LO https://gist.githubusercontent.com/tahsinrahman/db0626153488f88ceac544404f33cc0f/raw/f9ba010b5dd194dbbf96f1431e5d8a46966ed79a/entrypoint.sh && \
    chmod +x entrypoint.sh && \
    mv entrypoint.sh /bin/

# install kubectl
#RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.10.5/bin/linux/amd64/kubectl &> /dev/null && \
COPY kubectl ./kubectl
RUN chmod +x ./kubectl && \
    mv ./kubectl /bin/

# install onessl
RUN curl -fsSL -o onessl https://github.com/kubepack/onessl/releases/download/0.3.0/onessl-linux-amd64 \
  && chmod +x onessl \
  && mv onessl /usr/local/bin/

CMD docker run --rm -it hello-world