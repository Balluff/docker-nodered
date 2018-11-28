# Use the Node.js Alpine container image
FROM alpine:3.8

# Update package repo and the system itself
RUN apk update && apk upgrade

# Install some necessary tools because some nodes needs to be rebuild
RUN apk add git make gcc g++ python npm nodejs

# Install Node-RED described in the official documentation
RUN npm install npm@latest -g
RUN npm install -g --unsafe-perm node-red@latest node-red-admin@latest

# Create a new user and create the default Node-RED directory. Change the users owner rights.
RUN adduser --disabled-password --gecos '' node-red \
    && mkdir /home/node-red/.node-red/ \
    && chown -R node-red:node-red /home/node-red/.node-red/

# Switch to the .node-red directory
WORKDIR /home/node-red/.node-red
COPY package.json /home/node-red/.node-red
# Install additional npm packages
RUN npm install

# Free up disk space and delete unneccessary tools and the apk cache
RUN apk del make gcc g++ python \
    && rm -rf /var/cache/apk/*

# Copy the default settings config to the users Node-RED default directory
RUN cp /usr/lib/node_modules/node-red/settings.js /home/node-red/.node-red/settings.js

# Provide the Node-RED volume for later mount bindings
VOLUME /home/node-red/.node-red

# Expose the default Node-RED port
EXPOSE 1880

# At this stage: Use the "node-red" user
USER node-red

# Define the entrypoint and start Node-RED
ENTRYPOINT [ "node-red" ]