FROM node:20-alpine AS base

RUN apk update && apk add --no-cache libc6-compat

WORKDIR /app

# global tools
RUN yarn global add turbo

# copy repo
COPY . .

# install dependencies
RUN yarn install

# set up medusa user
RUN addgroup --system --gid 1001 medusa
RUN adduser --system --uid 1001 medusa
RUN mkdir -p /app/apps/backend/static
RUN chown -R medusa:medusa /app/apps/backend

USER medusa

WORKDIR /app/apps/backend

# veritabanı tablolarını oluştur
RUN npx medusa db:setup

# start komutu
CMD ["npx", "medusa", "start", "--types=false", "-p", "9000"]
