# Stage 1: Build stage
FROM node:18 AS build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json (or yarn.lock) first
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the application if necessary (e.g., transpiling TypeScript or bundling assets)
# RUN npm run build

# Stage 2: Production stage
FROM node:18-slim

# Set the working directory in the container
WORKDIR /app

# Copy only the necessary files from the build stage
COPY --from=build /app/node_modules /app/node_modules
COPY --from=build /app /app

# Expose port 7000
EXPOSE 7000

# Set the entry point for the container
ENTRYPOINT ["node", "server.js"]
