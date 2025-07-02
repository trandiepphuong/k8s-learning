## build stage ##
FROM --platform=linux/amd64 node:18.18-alpine as build

WORKDIR /app
COPY . .

RUN npm install --force
RUN npm run build

## run stage ##
FROM --platform=linux/amd64 nginx:alpine

COPY --from=build /app/dist/angular-ecommerce /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
