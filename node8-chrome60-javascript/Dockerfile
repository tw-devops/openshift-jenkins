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

# https://hub.docker.com/r/markadams/chromium-xvfb-js/~/dockerfile/
WORKDIR /usr/src/app
ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 8.x
ENV YARN_VERSION 1.1.0

RUN curl -sL https://deb.nodesource.com/setup_${NODE_VERSION} | bash - \
    && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists
RUN curl -o- -L https://yarnpkg.com/install.sh | bash -s -- --version ${YARN_VERSION}
CMD npm test

ONBUILD COPY package.json /usr/src/app/package.json
ONBUILD RUN npm install
ONBUILD COPY . /usr/src/app
