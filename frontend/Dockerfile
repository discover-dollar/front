# ---------- Build Angular App ----------
FROM node:20.9.1
ENV GENERATE_SOURCEMAP=false
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install @types/node@18 typescript@4.9
COPY . .
RUN npm run build -- --configuration production

# The production build will be in /app/dist/angular-15-crud
# You can copy it to your server's webroot directly
