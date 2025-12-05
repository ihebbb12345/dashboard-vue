# -------- BUILD STAGE ----------
FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm install --production=false

COPY . .
RUN npm run build

# -------- RUNTIME STAGE ----------
FROM node:20-alpine

WORKDIR /app

COPY --from=build /app/.output ./.output

ENV NITRO_PORT=8080
ENV PORT=8080
EXPOSE 8080

CMD ["node", ".output/server/index.mjs"]
