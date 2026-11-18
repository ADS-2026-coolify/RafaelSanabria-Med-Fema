FROM node:24-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY angular.json tsconfig*.json ./
COPY public ./public
COPY scripts ./scripts
COPY src ./src
RUN MEDFEMA_API_URL=/api npm run build

FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist/frontend/browser/ /usr/share/nginx/html/
EXPOSE 80
