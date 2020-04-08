FROM node:alpine AS build
WORKDIR /usr/src

# dependencies
COPY package.json /usr/src/
RUN npm install

# App
COPY . /usr/src
RUN npm run build

FROM nginx:alpine AS app

COPY nginx/default.conf /etc/nginx/conf.d/default.conf

COPY --from=build /usr/src/dist /usr/share/nginx/html

VOLUME ["/var/cache/nginx"]
