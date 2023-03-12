FROM node:16-alpine

RUN corepack enable
WORKDIR /my-app
COPY .  /my-app/

RUN pnpm i
RUN pnpm build
CMD pnpm start
