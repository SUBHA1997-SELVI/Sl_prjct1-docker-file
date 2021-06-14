### STAGE1:build ###
FROM node:12.7-alpine AS build
WORKDIR  /usr/src/app
COPY package.json package-lock.json ./
RUN npm install
copy . .
RUN npm run build

### STAGE2: RUN ###
FROM nginx:stable-alpine
COPY nginx.conf  /etc/nginx/nginx.conf
COPY --from-build /usr/src/app/dist /aston-villa-app /usr/share/nginx/html
