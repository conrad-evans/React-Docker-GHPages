FROM node:14.17.0-alpine as base

WORKDIR /app

COPY ./package*.json .
COPY ./yarn.lock .

RUN  yarn install --frozen-lockfile --non-interactive || exit 1
COPY . .

ENV CI=true
RUN yarn test --coverage

RUN yarn build

FROM ngnix
EXPOSE 80
COPY --from=base /app/build /usr/share/nginx/html


