FROM jenkins/jenkins:lts-jdk17

USER root

# Install Maven, Git and Docker
RUN apt-get update && apt-get install -y \
    maven \
    git \
    ca-certificates \
    curl \
    sudo && \
    curl -fsSL https://get.docker.com -o install-docker.sh && \
    sh install-docker.sh && \
    usermod -aG docker jenkins && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

USER jenkins

EXPOSE 8080
