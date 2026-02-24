# Stage: Angular dev container
FROM node:16.20.0

WORKDIR /app

# Install Angular CLI globally
RUN npm install -g @angular/cli

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Expose Angular dev server port
EXPOSE 8081

# Run Angular dev server
CMD ["ng", "serve", "--host", "0.0.0.0", "--port", "8081", "--disable-host-check"]
