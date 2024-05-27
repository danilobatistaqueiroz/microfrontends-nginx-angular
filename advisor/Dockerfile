### STAGE 1:BUILD ###
FROM node:20.5.0-alpine AS build

WORKDIR /dist/src/app
RUN npm cache clean --force

COPY . .
RUN rm -Rf node_modules/.pnpm
RUN npm install -g npm@10.8.0
RUN npm install
RUN npm run build --prod -- --base-href /advisor/

### STAGE 2:RUN ###
FROM nginx:latest AS ngi

COPY --from=build /dist/src/app/dist/advisor/browser /usr/share/nginx/html
COPY ./config/nginx.conf /etc/nginx/nginx.conf

EXPOSE 80