# Stage 1: Build the React application
FROM node:14 as build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Stage 2: Serve the built React application using a Node.js server
FROM node:14

# Set working directory
WORKDIR /frontend

# Copy build output from Stage 1
COPY --from=build /frontend/dist ./dist

# Install serve globally to serve static files
RUN npm install -g serve

# Expose port 3000 (or any other port your Node.js server will use)
EXPOSE 80

# Command to run the application
CMD ["serve", "-s", "build", "-l", "80"]
