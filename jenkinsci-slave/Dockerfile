# The MIT License
#
#  Copyright (c) 2015, CloudBees, Inc.
#
#  Permission is hereby granted, free of charge, to any person obtaining a copy
#  of this software and associated documentation files (the "Software"), to deal
#  in the Software without restriction, including without limitation the rights
#  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
#  copies of the Software, and to permit persons to whom the Software is
#  furnished to do so, subject to the following conditions:
#
#  The above copyright notice and this permission notice shall be included in
#  all copies or substantial portions of the Software.
#
#  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
#  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
#  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
#  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
#  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
#  THE SOFTWARE.

FROM kodbasen/java-jdk-arm:jdk-8u111-b14

ENV HOME /home/jenkins
ENV NVM_DIR $HOME/.nvm
RUN groupadd -g 10000 jenkins
RUN useradd -c "Jenkins user" -d $HOME -u 10000 -g 10000 -m jenkins

ARG VERSION=3.7

RUN apt-get update \
  && apt-get -y install bash git curl zip \
  && curl -o- https://yarnpkg.com/install.sh | bash \
  && curl --create-dirs -ksSLo /usr/share/jenkins/slave.jar https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/${VERSION}/remoting-${VERSION}.jar \
  && chmod 755 /usr/share/jenkins \
  && chmod 644 /usr/share/jenkins/slave.jar \
  && apt-get clean \
  && curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash \
  && chmod 755 $NVM_DIR/nvm.sh \
  && [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" \
  && nvm install v7.9.0 \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY jenkins-slave.sh /usr/local/bin/jenkins-slave

RUN chmod +rx /usr/local/bin/jenkins-slave

VOLUME /home/jenkins

WORKDIR /home/jenkins

USER jenkins

ENTRYPOINT ["jenkins-slave"]
