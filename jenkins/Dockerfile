FROM jenkins/jenkins:jdk17
USER root

# SET ENVIRONMENT VARS FOR NODE VERSION AND DIRECTORY
ENV NODE_VERSION=20.14.0
ENV NVM_DIR=/usr/local/nvm

# CREATE NODE DIRECTORY
RUN mkdir ${NVM_DIR}

# INSTALL CURL
RUN apt-get update \
  && apt-get install -y curl \
  && apt-get clean

# DOWNLOAD AND INSTALL NVM
RUN curl -s https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash \
  && . ${NVM_DIR}/nvm.sh \
  && nvm install ${NODE_VERSION} \
  && nvm alias default ${NODE_VERSION} \
  && nvm use default

# ADD NODE TO THE PATH ENVIRONMENT VARS
ENV NODE_PATH ${NVM_DIR}/v${NODE_VERSION}/lib/node_modules
ENV PATH ${NVM_DIR}/versions/node/v${NODE_VERSION}/bin:${PATH}

# CHECK IF NODE HAS INSTALLED
RUN node -v
RUN npm -v

# CHANGE PERMISSIONS FOR JENKINS USE
RUN chown -R jenkins:jenkins ${NVM_DIR}

USER jenkins