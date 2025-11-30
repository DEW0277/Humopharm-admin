FROM node:20-slim
WORKDIR /app
RUN npm config set registry https://registry.npmmirror.com
RUN apt-get update && apt-get install -y openssl ca-certificates && rm -rf /var/lib/apt/lists/*
COPY package*.json ./
RUN npm install
COPY prisma ./prisma
COPY . .
RUN npx prisma migrate
RUN npm run build
CMD ["sh", "-c", "npx prisma migrate deploy && npm run start:dev"]
#CMD ["npm", "run", "start:dev"]
