# Backend Dockerfile
FROM node:20-alpine

WORKDIR /app

# Copy root package files (backend dependencies are defined here)
COPY package*.json ./

# Install production dependencies
RUN npm install 

# Copy backend source code and uploads folder
COPY backend/ ./backend/
COPY uploads/ ./uploads/

# Expose backend port
EXPOSE 5000

# Start backend server
CMD ["node", "backend/server.js"]
