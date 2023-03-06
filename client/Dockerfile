FROM node:16.16.0 as dependencies

RUN mkdir -p /var/www/client/node_modules

RUN chown -R node:node /var/www/client

WORKDIR /var/www/client

ADD ./app/package.json ./

RUN yarn install \
  # --frozen-lockfile \
  --non-interactive \
  --production=false


FROM node:16.16.0 as builder

WORKDIR /var/www/client

ADD ./app ./

COPY --from=dependencies /var/www/client/node_modules ./node_modules

RUN yarn build

RUN yarn autoclean


FROM node:16.16.0 as runner

WORKDIR /var/www/client

ADD ./app/package.json ./

ADD ./app/nuxt.config.js ./

COPY --from=builder ./app/node_modules ./node_modules/
COPY --from=builder ./app/.nuxt ./.nuxt/
COPY --from=builder ./app/src/static ./src/static/

ENV NODE_ENV production

ENV HOST 0.0.0.0

EXPOSE 8080

COPY --chown=node:node ./app .



CMD [ "yarn", "start" ]
