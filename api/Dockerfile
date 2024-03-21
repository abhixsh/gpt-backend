# Use a base image with Node.js pre-installed
FROM node:18-alpine

# Set the working directory in the container
WORKDIR /api

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Expose the port your app runs on
EXPOSE 3000

# Command to run your app
CMD ["npm", "start"]