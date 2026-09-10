FROM node:22-slim AS build

WORKDIR /app

COPY web/package.json ./
RUN npm install

COPY web/ ./

ARG API_URL=http://api:4000
ENV API_URL=${API_URL}

RUN npm run build

FROM node:22-slim

WORKDIR /app
ENV NODE_ENV=production

COPY --from=build /app/.next/standalone ./
COPY --from=build /app/.next/static ./.next/static

EXPOSE 3000

CMD ["node", "server.js"]
