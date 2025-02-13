# Use the official Node.js image
FROM node:16

# Create and set the working directory
WORKDIR /usr/src/app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install 

# Copy the rest of the application code
COPY . .

# Expose port 8080 for the WebSocket server
EXPOSE 8080

# Start the application
CMD [ "npm", "start" ]

