# Stage 1: Build Angular App
FROM node:16.20.0 AS build

WORKDIR /app

# Copy package files and install dependencies
COPY package.json package-lock.json ./
RUN npm install

# Copy the rest of the code and build
COPY . .
RUN npm run build --prod

# Stage 2: Serve built files with a lightweight static server
FROM node:16.20.0

WORKDIR /app

# Install serve globally
RUN npm install -g serve

# Copy build output from previous stage
COPY --from=build /app/dist /app/dist

# Expose port for container
EXPOSE 8081

# Start the static server
CMD ["serve", "-s", "dist", "-l", "8081"]
