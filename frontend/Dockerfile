# Stage 1: build the Angular app
FROM node:16.20.0
ENV GENERATE_SOURCEMAP=false
WORKDIR /app
COPY package.json package-lock.json ./
COPY . .
RUN npm install
RUN npm run build

# Stage 2: serve using built-in Angular dev server
CMD ["npx", "serve", "-s", "dist/<project-name>", "-l", "8081"]
