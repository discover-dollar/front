# Use Node 20 (Angular 15 compatible)
FROM node:20.9.1

# Set working directory
WORKDIR /app

# Copy package files
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install @types/node@18 typescript@4.9
COPY . .

# Expose Angular dev server port
EXPOSE 8081

# Run Angular dev server
CMD ["npx", "ng", "serve", "--host", "0.0.0.0", "--port", "8081"]
