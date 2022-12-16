ARG REPO=balmydiamond0u/development-environment
FROM $REPO:arm64_ubuntu22.04_dotnet7.0

USER root

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && sudo ./aws/install \
    && rm awscliv2.zip \
    && rm -r ./aws

RUN curl -fsSL https://deb.nodesource.com/setup_19.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g aws-cdk

USER developer
