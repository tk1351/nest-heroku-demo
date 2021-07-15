FROM node:14.16.0 As development

WORKDIR /api

COPY ./api/package.json ./

RUN yarn install --only=development

COPY . .

RUN yarn build

FROM node:14.16.0 As production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR /api

COPY package.json ./

RUN yarn install --only=production

COPY . .

COPY --from=development /app/dist ./dist

CMD ["node", "dist/main"]