FROM node:24-slim
WORKDIR /app
RUN npm config set registry https://registry.npmmirror.com
RUN apt-get update && apt-get install -y openssl ca-certificates && rm -rf /var/lib/apt/lists/*
COPY package*.json ./
RUN npm install
COPY prisma ./prisma
COPY . .
RUN npx prisma migrate dev --name init
RUN npm run seed
RUN npm run build
CMD ["npm", "run", "start:dev"]
