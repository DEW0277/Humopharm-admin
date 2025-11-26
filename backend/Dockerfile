FROM node:20-alpine
WORKDIR /app
RUN apk add --no-cache openssl
COPY package*.json ./
RUN npm install
COPY prisma ./prisma
COPY . .
RUN npx prisma generate
CMD ["node", "dist/src/main.js"]
