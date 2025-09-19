# See here for image contents: https://github.com/devcontainers/images/tree/main/src/python
# Available image variants: https://github.com/devcontainers/templates/blob/main/src/python/devcontainer-template.json
ARG VARIANT="3"
FROM mcr.microsoft.com/devcontainers/python:1-${VARIANT}-bookworm

# [Option] Install Node.js
# ARG INSTALL_NODE="true"
# ARG NODE_VERSION="lts/*"
# RUN if [ "${INSTALL_NODE}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi

# [Optional] If your pip requirements rarely change, uncomment this section to add them to the image.
# COPY requirements.txt /tmp/pip-tmp/
# RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
#    && rm -rf /tmp/pip-tmp

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1

# Install OpenJDK-17
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends openjdk-17-jdk

# Create directory and set permission.
RUN mkdir /home/vscode/dev \ 
    && chown -R vscode:vscode /home/vscode/dev

# Install dev requirements
COPY ./dev/requirements_dev.txt /tmp/pip-tmp/
RUN pip3 --disable-pip-version-check --no-cache-dir install --upgrade -r /tmp/pip-tmp/requirements_dev.txt \
   && rm -rf /tmp/pip-tmp

# [Option] Download Kotlin LSP for VS Code
ARG DOWNLOAD_KOTLIN_LSP="true"
ARG KOTLIN_LSP_VERSION="0.253.10629"
RUN if [ "${DOWNLOAD_KOTLIN_LSP}" = "true" ]; then su vscode -c "cd /home/vscode && curl -L https://download-cdn.jetbrains.com/kotlin-lsp/${KOTLIN_LSP_VERSION}/kotlin-${KOTLIN_LSP_VERSION}.vsix -o kotlin-lsp.vsix"; fi
