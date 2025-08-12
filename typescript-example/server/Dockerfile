# Use Node.js 18 LTS as the base image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci --only=production

# Copy source code
COPY src/ ./src/
COPY tsconfig.json ./

# Install dev dependencies for build
RUN npm ci

# Build TypeScript
RUN npm run build

# Remove dev dependencies to reduce image size
RUN npm prune --production

# Note: Port will be determined by $PORT env var at runtime (defaults to 8080)

# Start the application
CMD ["node", "build/index.js"]

# Expose a PORT 
EXPOSE 3000
