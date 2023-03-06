FROM nginx:1.19.0-alpine

RUN rm -rf /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx/conf.d

WORKDIR /var/www

RUN mkdir -p /var/www/cache

RUN chown -R nginx:nginx /var/www/cache
