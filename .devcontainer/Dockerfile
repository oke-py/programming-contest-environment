FROM ruby:2.7.1-slim-buster as ruby
FROM mcr.microsoft.com/devcontainers/python:0-3-bullseye

COPY --from=ruby /usr/local/bin/ruby /usr/local/bin/
COPY --from=ruby /usr/local/bin/gem /usr/local/bin/
COPY --from=ruby /usr/local/lib/libruby.so.2.7 /usr/local/lib/
COPY --from=ruby /usr/local/lib/ruby /usr/local/lib/ruby

# git
COPY vscode-dev-containers/script-library/git-from-src-debian.sh /tmp/library-scripts/
RUN apt-get update && bash /tmp/library-scripts/git-from-src-debian.sh

# node
ENV NVM_DIR="/usr/local/share/nvm"
ENV NVM_SYMLINK_CURRENT=true \
    PATH=${NVM_DIR}/current/bin:${PATH}
COPY vscode-dev-containers/script-library/node-debian.sh /tmp/library-scripts/
RUN apt-get update && bash /tmp/library-scripts/node-debian.sh "${NVM_DIR}"

# programming contest
RUN echo "alias ojt='oj t -c \"ruby main.rb\"'" >> /home/vscode/.bashrc
RUN pip3 install online-judge-tools
RUN npm install -g atcoder-cli
COPY --chown=vscode:vscode atcoder-cli-nodejs /home/vscode/.config/atcoder-cli-nodejs
