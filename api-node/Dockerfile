FROM node:3.16-alpine as base

WORKDIR /usr/src/app

COPY package*.json ./

FROM base as dev

COPY . .

CMD ["npm", "run", "dev"]

FROM base as prod

ENV NODE_ENV=production 

RUN --type=mount=cache,target=/usr/src/app/.npm \
    npm set cache /usr/src/app/.npm && \    
    npm ci --only=production 

USER node

COPY --chown=node:node ./healhcheck.js ./

COPY --chown=node:node ./src/ .

EXPOSE 8080

CMD ["node", "index.js"]