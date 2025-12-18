FROM mcr.microsoft.com/devcontainers/java:dev-21-jdk-bookworm

ARG INSTALL_MAVEN="false"
ARG MAVEN_VERSION=""

ARG INSTALL_GRADLE="true"
ARG GRADLE_VERSION=""

ARG DOCKER_GROUP=989

RUN groupadd -f docker -g $DOCKER_GROUP
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends zip unzip maven curl docker.io postgresql-client
RUN usermod -aG docker vscode

RUN if [ "${INSTALL_MAVEN}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install maven \"${MAVEN_VERSION}\""; fi \
    && if [ "${INSTALL_GRADLE}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/sdkman/bin/sdkman-init.sh && sdk install gradle \"${GRADLE_VERSION}\""; fi

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1
