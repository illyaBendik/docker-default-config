FROM node:16.16.0-alpine

RUN mkdir -p /var/www/server/node_modules && chown -R node:node /var/www/server

WORKDIR /var/www/server

COPY ./app/package.json ./

ENV NODE_ENV=production

RUN yarn install \
  --prefer-offline \
  --pure-lockfile \
  --non-interactive \
  --production=true

EXPOSE 3005

COPY --chown=node:node ./app .

USER node

CMD [ "node", "app.js" ]
