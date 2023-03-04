FROM node:16.16.0 as builder

RUN mkdir -p /var/www/client
WORKDIR /var/www/client

COPY . .

RUN yarn install \
  --prefer-offline \
  # --frozen-lockfile \
  --non-interactive \
  --production=false

RUN rm -rf yarn.lock

RUN yarn build

RUN rm -rf node_modules && \
  NODE_ENV=production yarn install \
  --prefer-offline \
  --pure-lockfile \
  --non-interactive \
  --production=true

FROM node:16.16.0

WORKDIR /var/www/client

COPY --from=builder /var/www/client/  .

ENV HOST 0.0.0.0
EXPOSE 3000

CMD [ "yarn", "start" ]