# Azure-ContainerApp-Continuous-Deployment-Using-GitHub-Actions

**In this, I will take you through setting up a GitHub Actions workflow for continuous deployment of a FastAPI application using Docker and Azure Container Apps. FastAPI is a modern web framework known for its high performance and ease of use. In this scenario, we will automate the process of logging into your Azure account, building the FastAPI app into a Docker image, pushing the image to Azure Container Registry (ACR), and deploying the container to Azure Container Apps. This solution ensures seamless continuous deployment, automatically updating your application with each new commit, offering both scalability and agility for modern cloud-native applications.**

![](/Images/GitHubActions.jpg)

<h3>Prerequisites</h3>
<h3>To set up the continuous deployment pipeline for your FastAPI application using GitHub Actions, you will need the following:</h3>

- **Azure Account** 
- **Azure Container Registry (ACR)** 
- **Azure Container App** 
- **Azure App Registration** 
- **GitHub**
- **Docker**
- 
> [!IMPORTANT]
> Step 1 to Step 4 is the manual setup. Automatic deployment will start from the Step 5.

<h2>Step 1: Create a Sample FastAPI Project with .env and requirements.txt</h2>

- **Create a project directory: First, create a new directory for your FastAPI project:**
  
      mkdir fastapi-sample
      cd fastapi-sample
  
- **Create a main.py file: Inside the project directory, create a file named main.py:**

      vim main.py
  
- **Add the following code to main.py:**

      from fastapi import FastAPI
      import os

      app = FastAPI()

      @app.get("/")
      def read_root():
          return {"message": "Welcome to FastAPI", "environment": os.getenv("ENVIRONMENT", "development")}

This code creates a simple FastAPI application that reads an environment variable (ENVIRONMENT) from a .env file.

- **Create a .env file: Create a .env file to store environment variables:**

      vim .env
  
- **Add the following content to the .env file:**

      ENVIRONMENT=production

- **Create a requirements.txt file: To make sure all dependencies are easily managed, create a requirements.txt file:**

      vim requirements.txt
  
- **Add the installed dependencies to this file:**

      fastapi
      uvicorn
      python-dotenv  # Needed to load environment variables from .env

**Congrats! 🎉 Your FastAPI application has been successfully developed.**
**Next, we can proceed with containerizing the application using Docker.**

- **Create a docker directory inside your fastapi-sample directory:**

      mkdir docker
      cd docker

- **Create a Dockerfile:**

      vim Dockerfile

- **Add the following code in Dockerfile:**

      FROM python:3.11.2

      WORKDIR /app

      RUN apt-get update && apt-get install -y \
          locales \
          locales-all

      COPY ./requirements.txt /app/requirements.txt

      RUN pip install --no-cache-dir --upgrade -r /app/requirements.txt

      COPY . /app/
      COPY .env /app/
      COPY ./docker /app/docker

      ENV TZ=Asia/Kolkata
      RUN chmod +x /app/docker/run.sh

      EXPOSE 8000

      ENTRYPOINT ["/app/docker/run.sh"]

- **Create a run.sh file that will help to run the FastAPI server on start of new container:**

      vim run.sh

- **Add the following code in run.sh:**

      #!/bin/sh
      cd /app/
      uvicorn app:app --host 0.0.0.0
**Congrats! 🎉 You have successfully containerized your FastAPI application.**

<h2>Step 2: Create the Azure Container Registry (ACR)</h2>

- In Azure dashboard navigate to **Search > Container Registry > Create.**

![](/Images/search-ACR.png)

Enter the name of your Azure Container Registry.

![](/Images/create-ACR.png)

- **Let's have a overview of Azure Container Registry.**

![](/Images/overview-ACR.png)
- This is the login server name by which you can login to your ACR.

**Congrats! 🎉 You have successfully created your Azure Container Registry (ACR).**

<h2>Step 3: Login and push the image to the ACR.</h2>

- **Login to the ACR using the command below:**

      docker login mycontainerregistry.azurecr.io
  
- **You will prompted to enter username and password to login:**
- **Navigate to the Access key tab in your registry dashboard:**
- **You will find the login username and password, enter the username and password:**
- **Inside the fastapi-sample run the below docker command to build the image:**

      docker build -t mycontainerregistry.azurecr.io/hello-world:latest -f docker/Dockerfile .

> [!NOTE]
> Be sure to include the ACR server name in your Docker image, as demonstrated above.

- **Now push the Image to your Azure Container Registry (ACR):**

      docker push mycontainerregistry.azurecr.io/hello-world:latest

![](/Images/repo-ACR.png)

**Congrats! 🎉 You have successfully pushed the image to your Azure Container Registry (ACR).**


<h2>Step 4: Create the Azure Container App</h2>

> [!NOTE]
> Create the Azure Container App within the same resource group, region and subscription as the Azure Container Registry (ACR).

- In Azure dashboard navigate to **Search > Container App > Create.**
- Choose the Subscription.
- Choose the resource group.
- Enter the name of your Container App.
- Choose Deployment source as **container image**.
- Choose region.
- Click next.
- Enter Container name.
- Select image source as ACR.
- Select subscription.
- Select registry that you have created.
- Select image for which you want to deploy the container app with its respective tag.
- Click next.
- Enable the ingress.
- Allow external traffic.
- Select Ingress type as HTTP.
- Mention the target port on which the application will run inside the container (let say 8000 for FastAPI).
- Click create.

**Congrats! 🎉 You have successfully created the Azure Container App taking the image source as Azure Container Registry (ACR).**
