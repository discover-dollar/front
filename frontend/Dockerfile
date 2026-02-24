#stage1 Build the application
FROM node:16.20.0
ENV GENERATE_SOURCEMAP=false
WORKDIR /app
COPY package.json .
COPY package-lock.json .
COPY . .
RUN npm cache clean --force
RUN npm install
RUN npm run build
# stage2 serve the application using nginx

FROM nginx:latest
COPY --from=0 /app/build /usr/share/nginx/html
EXPOSE 80
EXPOSE 443
ENV NODE_ENV production
ENV PORT 80
CMD ["nginx", "-g", "daemon off;"]
