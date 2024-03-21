<h1>Step 1: Set Up Your Development Environment</h1>

- Ensure you have Docker installed on your system. You can download and install them from their respective websites.

<h1>Step 2: Containerize Your Application with Docker</h1>

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
<h1>Step 3: Build and Test Your Docker Image Locally</h1>

- Open a terminal, navigate to the root directory of your project, and execute the following commands:

```
#Check the installation
docker
```
```
# Build the Docker image
docker build -t gptbackend:v1 .
```
```
#See docker images
docker images
```
```
Tag the image
docker tag <image-name> <docker-id>/<image-name>
```
```
# Run the Docker container
docker run -p 3000:3000 gptbackend:v1
```

- Verify that your application is running correctly by accessing http://localhost:3000 in your web browser.

<h1>Step 4: Set Up Azure Resources</h1>

<h3>Create an Azure Account:</h3>

Sign up for an Azure account if you haven't already. You can get started with a free account that includes credits to explore Azure services.

<h3>Install Azure CLI:</h3>

Install Azure CLI on your local machine. This command-line tool will allow you to interact with Azure services from your terminal.

<h1>Step 5: Create a registry in Azure Container Registry</h1>

1. Sign in to the Azure portal with your Azure subscription.

2. On the Azure portal home page, under Azure services, select Create a resource. The Create a resource pane appears.

3. In the left menu pane, select Containers, and under Popular Azure services, select Container Registry.
![Screenshot that shows the New pane in Azure portal showing the Container options available in Azure Marketplace.](https://learn.microsoft.com/en-us/training/modules/deploy-run-container-app-service/media/3-search-container-registry-annotated.png)

4. The <b>Create container registry</b> pane appears.

On the Basics tab, enter the following values for each setting.
| Setting      | Value |
| ----------- | ----------- |
| Project details      |        |
| Subscription   | Select your Azure subscription.        |
Resource group | Select Create new, and enter ```<nameoftheResourcegroup>```, and select OK.|
|Registry name|Enter a unique name and make a note of it for later.|
|Location||
|SKU||
|

5. Select <b>Review + create.</b> After validation successfully passes, select Create. Wait until the container registry has been created before you continue.


<h1>Step 6: Build a Docker image and upload it to Azure Container Registry</h1>


1. In Azure Cloud Shell in the portal (select the Cloud Shell icon on the upper toolbar), run the following command to download the source code for the sample web app. This web app is simple. It presents a single page that contains static text and a carousel control that rotates through a series of images.


```
git clone <Repo Link>
```

2. Move to the source folder.


```
cd <Source Folder>
```

3. Run the following command. This command sends the folder's contents to the Container Registry, which uses the instructions in the Docker file to build the image and store it. Replace <container_registry_name> with the name of the registry you created earlier. Take care not to leave out the . character at the end of the command.

```
az acr build --registry <container_registry_name> --image <imagename> .
```

The Docker file contains the step-by-step instructions for building a Docker image from the source code for the web app. Container Registry runs these steps to build the image, and as each step completes, a message is generated. The build process should finish after a couple of minutes without any errors or warnings.

<h3>Examine the container registry</h3>

1. Return to the Azure portal, and on the Overview page for your container registry, select Go to resource. Your Container registry pane appears.

2. In the left menu pane, under Services, select Repositories. The Repositories pane appears for your container registry. You'll see a repository named webimage.

3. Select the webimage repository. The webimage repository pane appears. It contains an image with the latest tag. This is the Docker image for the sample web app.![Screenshot that shows the repositories and images uploaded to Azure Container Registry.](https://learn.microsoft.com/en-us/training/modules/deploy-run-container-app-service/media/3-azure-container-repositories.png)


The Docker image that contains your web app is now available in your registry for deployment to App Service.
