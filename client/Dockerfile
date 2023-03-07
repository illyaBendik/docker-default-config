FROM node:16.16.0 as DEPENDENCIES

RUN mkdir -p /var/www/client/node_modules

RUN chown -R node:node /var/www/client

WORKDIR /var/www/client

ADD ./app/package.json ./

RUN yarn install \
  # --frozen-lockfile \
  --non-interactive \
  --production=false


FROM node:16.16.0 as BUILDER

WORKDIR /var/www/client

ADD ./app ./

COPY --from=dependencies /var/www/client/node_modules ./node_modules

RUN yarn build


FROM node:16.16.0 as RUNNER

WORKDIR /var/www/client

ADD ./app/package.json ./

ADD ./app/nuxt.config.js ./

COPY --from=BUILDER ./var/www/client/node_modules ./node_modules/
COPY --from=BUILDER ./var/www/client/.nuxt ./.nuxt/
COPY --from=BUILDER ./var/www/client/static ./static/

ENV NODE_ENV production
ENV NUXT_HOST 0.0.0.0
ENV NUXT_PORT 3000

EXPOSE 3000

COPY --chown=node:node ./app .

CMD [ "yarn", "start" ]
