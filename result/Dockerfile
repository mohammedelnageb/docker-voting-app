# Use a multi-stage build to optimize the final image size
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install --only=production

COPY . .
# second stage
FROM node:18-alpine

WORKDIR /app

ENV NODE_ENV=production

COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/server.js ./server.js
COPY --from=builder /app/views ./views
COPY --from=builder /app/package*.json ./

EXPOSE 4000

CMD ["node", "server.js"]
