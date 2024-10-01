FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

FROM node:18-alpine

ENV NODE_ENV=production

WORKDIR /app

RUN npm install -g pm2

COPY --from=builder /app ./

RUN npm install --only=production

EXPOSE 3000

CMD ["pm2-runtime", "npm", "--", "start"]
