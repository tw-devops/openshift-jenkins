FROM buildpack-deps:stretch-scm

# labels
LABEL description="Debian with node8 & chrome" \
      maintainer="https://github.com/tw-devops" \
      display-name="Debian Node8 & Chrome" \
      tags="debian,node8,yarn"

# https://hub.docker.com/r/markadams/chromium-xvfb/~/dockerfile/
RUN apt-get update && apt-get install -y curl xvfb chromium

ADD xvfb-chromium /usr/bin/xvfb-chromium
RUN ln -s /usr/bin/xvfb-chromium /usr/bin/google-chrome
RUN ln -s /usr/bin/xvfb-chromium /usr/bin/chromium-browser

# install nodejs and yarnpkg
RUN apt-get install xz-utils
ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 8.6.0
ENV YARN_VERSION 1.1.0

RUN curl -SLO https://nodejs.org/dist/v8.6.0/node-v${NODE_VERSION}-linux-x64.tar.xz && \
    tar -Jxf node-v${NODE_VERSION}-linux-x64.tar.xz -C /usr/local/ --strip-components=1 && \
    rm node-v${NODE_VERSION}-linux-x64.tar.xz && \
    ln -s /usr/local/bin/node /usr/local/bin/nodejs

RUN npm install --global yarn@${YARN_VERSION}

CMD echo node=$(node -v), npm=$(npm -v), yarn=$(yarn -v)
