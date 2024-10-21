# Azure-ContainerApp-Continuous-Deployment-Using-GitHub-Actions

**In this, I will take you through setting up a GitHub Actions workflow for continuous deployment of a FastAPI application using Docker and Azure Container Apps. FastAPI is a modern web framework known for its high performance and ease of use. In this scenario, we will automate the process of logging into your Azure account, building the FastAPI app into a Docker image, pushing the image to Azure Container Registry (ACR), and deploying the container to Azure Container Apps. This solution ensures seamless continuous deployment, automatically updating your application with each new commit, offering both scalability and agility for modern cloud-native applications.**

![](/Images/GitHubActions.jpg)

<h3>Prerequisites</h3>
<h3>To set up the continuous deployment pipeline for your FastAPI application using GitHub Actions, you will need the following:</h3>

- **Azure Account:** 
- **Azure Container Registry (ACR):** 
- **Azure Container App:** 
- **Azure App Registration:** 
- **GitHub:**

<h2>Step 1: Create a Sample FastAPI Project with .env and requirements.txt</h2>

- **Create a project directory: First, create a new directory for your FastAPI project:**
  
      mkdir fastapi-sample
      cd fastapi-sample
  
- **Create a main.py file: Inside the project directory, create a file named main.py:**

      touch main.py
  
- **Add the following code to main.py:**

      from fastapi import FastAPI
      import os

      app = FastAPI()

      @app.get("/")
      def read_root():
          return {"message": "Welcome to FastAPI", "environment": os.getenv("ENVIRONMENT", "development")}

This code creates a simple FastAPI application that reads an environment variable (ENVIRONMENT) from a .env file.

- **Create a .env file: Create a .env file to store environment variables:**

      touch .env
  
- **Add the following content to the .env file:**

      ENVIRONMENT=production

- **Create a requirements.txt file: To make sure all dependencies are easily managed, create a requirements.txt file:**

      touch requirements.txt
  
- **Add the installed dependencies to this file:**

      fastapi
      uvicorn
      python-dotenv  # Needed to load environment variables from .env

**Congrats! 🎉 Your FastAPI application has been successfully developed.**


