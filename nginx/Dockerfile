FROM nginx:1.19.0-alpine

RUN rm -rf /etc/nginx/conf.d/default.conf

RUN mkdir -p /var/www/cache && chown -R nginx:nginx /var/www/cache

COPY --chown=nginx:nginx /var/www/cache /var/www/cache

COPY nginx.conf /etc/nginx/conf.d