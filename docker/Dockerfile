FROM node:22-alpine AS builder

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

RUN npm run build

FROM node:22-alpine

WORKDIR /app

COPY --from=builder /app/package.json .
COPY --from=builder /app/public ./public

RUN mkdir ".next"

COPY --from=builder /app/.next ./.next

RUN npm install --omit=dev

CMD ["npm", "start"]