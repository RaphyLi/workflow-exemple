FROM node:12.8.0 as build

# create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

ARG ENVIRONMENT
ARG VERSION
ARG API_URL
ARG GOOGLE_CLIENT_ID
ARG REDIRECT_URI

RUN npm install -g @angular/cli
RUN npm install

# Bundle app source
COPY . ./

RUN npm run build:$ENVIRONMENT

FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
# COPY .htpasswd /etc/nginx/.htpasswd
COPY --from=build /usr/src/app/dist /usr/share/nginx/html
