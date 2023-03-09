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

ENV NODE_ENV production
ENV NUXT_HOST 0.0.0.0
ENV NUXT_PORT 3000
ENV BASE_URL /
ENV API_URL http://bestbetontario.com/api/v1
ENV TINYMCE_API_KEY 5ogmlslbg8c7sza82f4fhjep32jxlqcmxoue1y1cwg8fwosj

ADD ./app ./

COPY --from=dependencies /var/www/client/node_modules ./node_modules

RUN yarn build


FROM node:16.16.0 as RUNNER

WORKDIR /var/www/client

RUN  mkdir -p ./store && touch ./store/index.js

USER node

ENV NODE_ENV production
ENV NUXT_HOST 0.0.0.0
ENV NUXT_PORT 3000
ENV BASE_URL /
ENV API_URL http://bestbetontario.com/api/v1
ENV TINYMCE_API_KEY 5ogmlslbg8c7sza82f4fhjep32jxlqcmxoue1y1cwg8fwosj

ADD --chown=node:node ./app/package.json ./
ADD --chown=node:node ./app/build.config.js ./
ADD --chown=node:node ./app/nuxt.config.js ./

COPY --chown=node:node --from=BUILDER ./var/www/client/node_modules ./node_modules/
COPY --chown=node:node --from=BUILDER ./var/www/client/.nuxt ./.nuxt/
COPY --chown=node:node --from=BUILDER ./var/www/client/static ./static/

EXPOSE 3000

CMD [ "yarn", "start" ]