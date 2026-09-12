#Build Stage
FROM node:20-alpine AS build
WORKDIR /usr/src/app
COPY package*.json .
RUN npm ci --omit=dev

#Runtime stage
FROM node:20-alpine
WORKDIR /usr/src/app
RUN addgroup -S -g 10001 appgroup && adduser -S -u 10001 appuser -G appgroup appuser
COPY --from=build --chown=appuser:appgroup /usr/src/app/node_modules ./node_modules
COPY . .
USER appuser
EXPOSE 5050
CMD ["npm", "start"]
