# Use Node.js 18 Alpine as base image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci --only=production

# Copy source code
COPY . .

# Add bash and wait-for-it
RUN apk add --no-cache bash

# Add wait-for-it script
ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh /wait-for-it.sh
RUN chmod +x /wait-for-it.sh

# Expose port 5000
EXPOSE 5000

# Start the application with wait-for-it (60 second timeout for maximum compatibility)
CMD ["/wait-for-it.sh", "db:3306", "--timeout=60", "--strict", "--", "node", "index.js"] 