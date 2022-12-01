FROM mcr.microsoft.com/devcontainers/python:0-3-bullseye

# git
# https://github.com/microsoft/vscode-dev-containers/blob/main/script-library/docs/git-from-src.md
COPY vscode-dev-containers/script-library/git-from-src-debian.sh /tmp/library-scripts/
RUN apt-get update && bash /tmp/library-scripts/git-from-src-debian.sh

# ruby
# https://github.com/microsoft/vscode-dev-containers/blob/main/script-library/docs/ruby.md
ENV GEM_PATH="/usr/local/rvm/gems/default:/usr/local/rvm/gems/default@global" \
    GEM_HOME="/usr/local/rvm/gems/default" \
    MY_RUBY_HOME="/usr/local/rvm/rubies/default" \
    PATH="/usr/local/rvm/rubies/default/bin:/usr/local/rvm/gems/default/bin:/usr/local/rvm/gems/default@global/bin:/usr/local/rvm/rubies/default/bin:/usr/local/rvm/bin:${PATH}"
COPY vscode-dev-containers/script-library/ruby-debian.sh /tmp/library-scripts/
RUN apt-get update && bash /tmp/library-scripts/ruby-debian.sh 2.7.1
RUN gem install rubocop solargraph

# node
# https://github.com/microsoft/vscode-dev-containers/blob/main/script-library/docs/node.md
ENV NVM_DIR="/usr/local/share/nvm"
ENV NVM_SYMLINK_CURRENT=true \
    PATH=${NVM_DIR}/current/bin:${PATH}
COPY vscode-dev-containers/script-library/node-debian.sh /tmp/library-scripts/
RUN apt-get update && bash /tmp/library-scripts/node-debian.sh "${NVM_DIR}"

# programming contest
RUN export PS1="\w $ "
RUN echo "alias ojt='oj t -c \"ruby main.rb\"'" >> /home/vscode/.bashrc
RUN pip3 install online-judge-tools
RUN npm install -g atcoder-cli
COPY --chown=vscode:vscode atcoder-cli-nodejs /home/vscode/.config/atcoder-cli-nodejs
