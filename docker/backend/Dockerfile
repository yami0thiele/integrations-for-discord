FROM node:21-alpine as local

RUN apk add --no-cache libc6-compat
WORKDIR /app

ENV NODE_ENV development

RUN yarn global add @nestjs/cli
COPY --chown=node:node ./backend .

RUN yarn --frozen-lockfile

USER node
