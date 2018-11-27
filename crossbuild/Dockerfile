# Use the Node.js Alpine container image
FROM resin/armv7hf-alpine:3.8

# Cross build based on: https://www.balena.io/docs/reference/base-images/base-images/#resin-xbuild-qemu
RUN [ "cross-build-start" ]

# Install some necessary tools because some nodes needs to be rebuild
RUN apk update && apk upgrade
#RUN apk add git make gcc g++ python linux-headers binutils-gold bash
RUN apk add git make gcc g++ python npm nodejs

# This section is necessary for import company CA certificates
# ARG certfile=./certs/

# Copy the certification files
# COPY ${certfile} /usr/local/share/ca-certificates/

# Update the certificates
# RUN update-ca-certificates

# Install Node-RED described in the official documentation
RUN npm i -g --unsafe-perm --verbose node-red@latest node-red-admin@latest
# Update npm packages used by Node-RED
RUN npm i -g --unsafe-perm --verbose mailparser@latest nodemailer@latest mimelib@latest mailcomposer@latest buildmail@latest bcrypt@latest node-uuid@latest cryptiles@latest boom@latest hoek@latest

# Create a new user
RUN adduser --disabled-password --gecos '' node-red
# Switch to the .node-red directory
WORKDIR /home/node-red/.node-red
# Install additional npm packages
RUN npm i --save --verbose winston@latest fs@latest macaddress@latest os@latest crypto@latest cron@latest moment@latest

RUN apk del make gcc g++ python \
    && rm -rf /var/cache/apk/*

# Delete the company certificates from the container image
# RUN rm -rf /usr/local/share/ca-certificates/ \
    # && update-ca-certificates

RUN [ "cross-build-end" ]

# Expose the default Node-RED port
EXPOSE 1880

VOLUME /home/node-red/.node-red
USER node-red

# Define the entrypoint and start Node-RED
ENTRYPOINT [ "node-red" ]