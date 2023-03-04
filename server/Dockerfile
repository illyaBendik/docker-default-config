FROM node:16.16.0 as builder

RUN mkdir -p /var/www/server
WORKDIR /var/www/server

COPY . .

USER node

RUN yarn install \
  --prefer-offline \
  --frozen-lockfile \
  --non-interactive \
  --production=false

COPY --chown=node:node . .

EXPOSE 3002

CMD [ "node", "app.js" ]
