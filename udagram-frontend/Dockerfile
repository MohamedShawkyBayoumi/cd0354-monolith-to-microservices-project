# ### Build
# FROM beevelop/ionic:latest AS ionic
# ## Create app directory
# WORKDIR /usr/src/app
# ## Install app dependencies
# ## A wildcard is used to ensure both package.json AND package-lock.json are copied
# COPY package*.json ./
# RUN npm ci
# ## Bundle app source
# COPY . .
# RUN ionic build
# ### Run 
# FROM nginx:alpine
# #COPY www /usr/share/nginx/html
# COPY --from=ionic  /usr/src/app/www /usr/share/nginx/html


# ### Build
# FROM node:18 AS ionic
# # Install Ionic CLI
# RUN npm install -g @ionic/cli
# ## Create app directory
# WORKDIR /usr/src/app
# ## Install app dependencies
# ## A wildcard is used to ensure both package.json AND package-lock.json are copied
# COPY package*.json ./
# # Run npm install with legacy-peer-deps and ignore platform-specific optional dependencies
# RUN npm ci --legacy-peer-deps --no-optional
# ## Set environment variable to fix OpenSSL issue
# ENV NODE_OPTIONS=--openssl-legacy-provider
# ## Bundle app source
# COPY . .
# RUN ionic build
# ### Run 
# FROM nginx:alpine
# #COPY www /usr/share/nginx/html
# COPY --from=ionic  /usr/src/app/www /usr/share/nginx/html

### Build
FROM node:18-alpine AS ionic
# Install necessary packages and Ionic CLI
RUN apk add --no-cache python3 make g++ && \
    npm install -g @ionic/cli
## Create app directory
WORKDIR /usr/src/app
## Install app dependencies
## A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package*.json ./
# Run npm install with legacy-peer-deps and ignore platform-specific optional dependencies
RUN npm ci --legacy-peer-deps --no-optional
## Set environment variable to fix OpenSSL issue
ENV NODE_OPTIONS=--openssl-legacy-provider
## Bundle app source
COPY . .
RUN ionic build
### Run 
FROM nginx:alpine
#COPY www /usr/share/nginx/html
COPY --from=ionic /usr/src/app/www /usr/share/nginx/html

