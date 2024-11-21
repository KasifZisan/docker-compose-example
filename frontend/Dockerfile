# Stage 1: Build Stage 
FROM node:11.10.0-alpine AS build-stage

RUN apk add --update --no-cache \
    python \
    make \
    g++

COPY . /src
WORKDIR /src
COPY ./package* ./
RUN npm install
RUN yarn build

#Stage 2: Docker Image for Prod Env

FROM nginx:latest
RUN rm -rf /usr/share/nginx/html
RUN mkdir /usr/share/nginx/html
COPY --from=build-stage /src/build/ /usr/share/nginx/html/
COPY default.conf /etc/nginx/conf.d/
EXPOSE 80
CMD ["nginx-debug", "-g", "daemon off;"]
