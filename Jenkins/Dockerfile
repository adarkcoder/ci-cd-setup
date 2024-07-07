# Start with the official Jenkins image
FROM jenkins/jenkins:lts

# Switch to root user
USER root

# Install Docker CLI, AWS CLI, and kubectl
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release software-properties-common unzip && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce-cli && \
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm -rf awscliv2.zip aws && \
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin/

RUN addgroup docker

# Allow Jenkins user to use Docker
RUN usermod -aG docker jenkins

# Switch back to Jenkins user
USER jenkins