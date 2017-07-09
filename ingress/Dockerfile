FROM node:latest

MAINTAINER andy99th <andy@99th.jp>

# Install hubot
RUN ln -s /usr/bin/nodejs /usr/bin/node \
 && npm install -g coffee-script \
 && npm install -g yo generator-hubot time cron

# Create user
RUN useradd -d /hubot -m -s /bin/bash -U hubot

# Change User and Directory
USER hubot
WORKDIR /hubot

# Setup hubot
RUN yo hubot --owner="andy99th" --name="HuBot" --description="HuBot on Docker" --defaults

# Install adapter and modules
RUN npm install --unsafe-perm --save git+https://github.com/thetimpanist/hubot-discord \
 && npm install --save lodash

# Install hubot tools
RUN npm install --save hubot-ingress \
 && npm install --save hubot-misawa \
 && sed -i 's/\[/\[\n  "hubot-ingress",\n  "hubot-misawa",/' external-scripts.json
 && sed -i '/hubot-heroku-keepalive/d' external-scripts.json

# Set script directory
VOLUME ["/hubot/scripts"]

# Run hubot
ENTRYPOINT ["bin/hubot"]
CMD ["-a", "discord", "--name", "'bot'"]
