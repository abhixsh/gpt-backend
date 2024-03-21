<h3>1. Create a Dockerfile:</h3>

- In the root directory of your project, create a file named Dockerfile with the following content:

```
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
```

<h3>2. Docker Deploy and run:</h3>

- Open a terminal, navigate to the root directory of your project, and execute the following commands:

```
docker -v
```
```
docker images
```
```
docker ps -a
```
```
docker build -t gptbackend:v1 .
```
```
docker run -p 3000:3000 gptbackend:v1
```

- Verify that your application is running correctly by accessing http://localhost:3000 in your web browser.


<h3>3. Connect Azure CLI:</h3>

- Open a terminal, navigate to the root directory of your project, and execute the following commands:

```
git clone https://github.com/abhixsh/gpt-backend
```
```
az acr build --registry gptbackend --image gptbackend:v1 .
```
```
az acr update --name gptbackend --admin-enabled true
```