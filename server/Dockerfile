FROM node:16.16.0-alpine

RUN mkdir -p /var/www/server/node_modules && chown -R node:node /var/www/server

WORKDIR /var/www/server

# ENV NODE_ENV=production
# ENV PORT=3002
# ENV MONGO_URI=mongodb+srv://illia:dGZ1ys6HFCoehVdZ@cluster0.vw42odg.mongodb.net/?retryWrites=true&w=majority
# ENV FILE_UPLOAD_PATH = ./public/uploads
# ENV MAX_FILE_UPLOAD = 2000000
# ENV JWT_SECRET="df5407da39ea6bbfb12c726f9929b3ecbf3b12f1695126ae77931ea15e99ee8c1d56da865b6a06b2d5341d191fceac787edab753601e08e0ceac3fcba090e099"
# ENV JWT_EXPIRE=3h
# ENV ADMIN_PASSWORD="pDnGkqaRx:))pa+C)B}@Fnhxoh8T0B>C>k)b@JPFFLW,)ke?_U:an8Xm7Qe^k0=ZV~2Qj_X7fhLMVZ9Y6rc]A.8MT47)c,},GpP#"

COPY ./app/ ./

RUN yarn install \
  --prefer-offline \
  --pure-lockfile \
  --non-interactive \
  --production=true

RUN yarn db:init

EXPOSE 3002

COPY --chown=node:node ./app .

USER node

CMD [ "node", "app.js" ]
