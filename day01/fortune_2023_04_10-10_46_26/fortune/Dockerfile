# ghcr.io/jane016/node:19
# (image repo/account name/image name:tag), the tag will change based on the new versions
# jane016/node:19 (account name, image name: tag) - implication is that it assume it is dockerhub (docker.io)
# node:19 (image name:tag) - assume is library/ in front
# if no tag, the default is latest, which is a bad practice, so never do that
# will only get node@sha256 after you publish the image

FROM node:19

# mkdir /app && cd /app
WORKDIR /app 

# copy the files
COPY main.js .
COPY package.json .
COPY package-lock.json .

# for directory need to give a name for the directory
COPY public public
COPY views views

# Install the node package
# npm i will get the latest packages (use for development)
# npm ci (will read from log file, use for CI only), CI doesn't look for updates, just install whatever you ask to install
# RUN ["npm", "ci"], does not have variable substitution as it doesnt go through the shell, more lightweight -> use in containers where there are no shell 

# run in shell
RUN npm ci 

# RUN
ENV APP_PORT=3000

# implement healthcheck 
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
  CMD curl localhost:${APP_PORT}/healthz || exit 1

EXPOSE ${APP_PORT}

ENTRYPOINT node main

# commands to run 
# docker build -t  jane016/cfdsa-fortune:1.0.0
# docker push jane016/cfdsa-fortune:1.0.0
# docker run -d -p 8080:3000 jane016/cfdsa-fortune:1.0.0
# docker ps
# docker rm -f <container name> 

# dive jane016/cfdsa-fortune:1.0.0
# docker run -d -e APP_PORT=5000 -p 8080:5000 jane016/cfdsa-fortune:1.0.0
# https://grafana.com/docs/loki/latest/clients/docker-driver/


