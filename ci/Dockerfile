FROM amazonlinux:2023

# Install required packages
RUN yum update -y && \
    yum install -y \
        unzip \
        curl \
        jq \
        tar \
        gzip \
        shadow-utils \
        docker && \
    yum clean all

# Install AWS CLI v2
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    rm -rf aws awscliv2.zip

# Verify installations
RUN aws --version && \
    docker --version && \
    jq --version

# Set working directory
WORKDIR /workspace

# Default command
CMD ["bash"]