FROM amazon/aws-cli:latest

# Install docker + jq
RUN yum install -y docker jq && yum clean all

# Verify
RUN aws --version && docker --version && jq --version

CMD ["sh"]