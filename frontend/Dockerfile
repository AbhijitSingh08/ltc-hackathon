# Stage 1: Build the React application
FROM node:18 AS build

# Set the working directory
WORKDIR /ltc-hackathon

# Copy frontend package.json and package-lock.json
COPY package.json package-lock.json ./frontend/

# Install dependencies for the frontend
RUN npm install --prefix frontend

# Copy the rest of the frontend code
COPY frontend ./frontend

# Build the React application
RUN npm run build --prefix frontend

# Stage 2: Setup Node.js server
FROM node:18

# Set the working directory
WORKDIR /ltc-hackathon

# Copy the built React files and Node.js server files
COPY --from=build /ltc-hackathon/frontend/dist ./dist
COPY backend/index.js ./index.js
COPY backend/package.json backend/package-lock.json ./

# Install Node.js server dependencies
RUN npm install

# Expose the port the app runs on
EXPOSE 80

# Command to run the Node.js server
CMD ["node", "index.js"]
