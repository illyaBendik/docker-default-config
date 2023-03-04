FROM nginx:1.19.0-alpine

RUN rm -rf /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx/conf.d

# COPY /certbot/conf /etc/letsencrypt

# COPY /certbot/www /var/www/certbot