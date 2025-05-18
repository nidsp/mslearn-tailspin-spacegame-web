# Use Ubuntu base image
FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Install required packages
RUN apt-get update && apt-get install -y \
    curl \
    apt-transport-https \
    ca-certificates \
    software-properties-common \
    unzip \
    jq \
    git \
    sudo \
    libcurl4 \
    libunwind8 \
    net-tools \
    libssl3 \
    libicu72 \
    libkrb5-3

# Set environment variables for agent version
ARG AGENT_VERSION=2.206.1
ARG ARCH=x64

# Download and extract Azure Pipelines agent
RUN mkdir -p /home/vscode/azure-pipelines \
    && cd /home/vscode/azure-pipelines \
    && curl -O -L https://vstsagentpackage.azureedge.net/agent/${AGENT_VERSION}/vsts-agent-linux-${ARCH}-${AGENT_VERSION}.tar.gz \
    && tar xzf vsts-agent-linux-${ARCH}-${AGENT_VERSION}.tar.gz \
    && ./bin/installdependencies.sh || true  # prevent crash on deprecated liblttng-ust0

# Optional: Set working directory and PATH for later use
WORKDIR /home/vscode/azure-pipelines
ENV PATH="${PATH}:/home/vscode/azure-pipelines"

# Set user
USER vscode
