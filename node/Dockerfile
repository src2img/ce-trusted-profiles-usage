FROM node:22-alpine

COPY package.json package-lock.json /app/
WORKDIR /app
RUN npm ci --omit=dev

COPY main.js /app

ENTRYPOINT ["node", "main.js"]
