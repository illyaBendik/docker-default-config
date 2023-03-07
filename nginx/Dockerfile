FROM nginx:1.19.0-alpine

COPY default.conf /etc/nginx/conf.d

# COPY nginx.conf /etc/nginx/

WORKDIR /var/www

RUN mkdir -p /var/www/cache

RUN chown -R nginx:nginx /var/www/cache
