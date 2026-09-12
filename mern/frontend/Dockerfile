#Build Stage
FROM node:20-alpine AS build
WORKDIR /usr/src/app
COPY package*.json .
RUN npm install
COPY . .
RUN npm run build

#Runtime stage
FROM node:20-alpine
WORKDIR /usr/src/app
RUN groupadd --system --gid 10001 appgroup && useradd --system --uid 10001 appuser --gid appgroup appuser
COPY --from=build --chown=appuser:appgroup /usr/src/app/dist ./dist
USER appuser
EXPOSE 5173
ENTRYPOINT ["npm"]
CMD ["start"]
