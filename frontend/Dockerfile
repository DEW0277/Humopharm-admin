FROM node:20-alpine AS builder
WORKDIR /app
COPY package.json package-lock.json yarn.lock* ./
RUN if [ -f package-lock.json ]; then \
      npm ci; \
    elif [ -f yarn.lock ]; then \
      yarn install; \
    else \
      npm install; \
    fi
COPY . .
RUN npm run build || yarn build

FROM nginx:1.29-alpine
RUN rm -rf /usr/share/nginx/html/*
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
