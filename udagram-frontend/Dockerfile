
### Build
FROM --platform=linux/amd64 beevelop/ionic AS ionic
## Create app directory
WORKDIR /usr/src/app
## Install app dependencies
## A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package*.json ./

ARG OPTS=--openssl-legacy-provider
ENV NODE_OPTIONS=$OPTS

CMD echo "NODE_OPTS: ${NODE_OPTIONS}"
RUN npm ci -f
## Bundle app source
COPY . .
 
RUN ionic build
### Run 
FROM nginx:alpine
#COPY www /usr/share/nginx/html
COPY --from=ionic  /usr/src/app/www /usr/share/nginx/html