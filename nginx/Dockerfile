FROM nginx:1.19.0-alpine

COPY default.conf /etc/nginx/conf.d

COPY nginx.conf /etc/nginx/

WORKDIR /var/www/

RUN mkdir -p ./cache

RUN chmod -R 777 /var/www/cache