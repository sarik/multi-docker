FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
#Dont have to export 3000 as client nginx is now listening on port3000(as set in default.conf and 
#since root nginx is also container,both can talk to each other directly like client:3000 without need to expose)
#expose is for telling host that this docker(client here ) listens on 3000 at runtime so host may map ports to it
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html