FROM node:14 AS builder
WORKDIR /usr/src/backend
COPY meta/package*.json ./
RUN npm set strict-ssl false && npm install --only=development
COPY meta/. .
RUN npm set strict-ssl false && npm run build

FROM node:14-slim AS production
ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}
WORKDIR /usr/src/backend
COPY --from=builder /usr/src/backend/package*.json ./
RUN  npm set strict-ssl false && npm install --only=production
COPY --from=builder /usr/src/backend/dist ./dist
CMD ["node", "dist/main"]
