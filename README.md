# Azure-ContainerApp-Continuous-Deployment-Using-GitHub-Actions

**In this, I will take you through setting up a GitHub Actions workflow for continuous deployment of a FastAPI application using Docker and Azure Container Apps. FastAPI is a modern web framework known for its high performance and ease of use. In this scenario, we will automate the process of logging into your Azure account, building the FastAPI app into a Docker image, pushing the image to Azure Container Registry (ACR), and deploying the container to Azure Container Apps. This solution ensures seamless continuous deployment, automatically updating your application with each new commit, offering both scalability and agility for modern cloud-native applications.**

![](/Images/GitHubActions.jpg)

<h3>Prerequisites</h3>
<h3>To set up the continuous deployment pipeline for your FastAPI application using GitHub Actions, you will need the following:</h3>

- **Azure Account:** A valid Azure account with sufficient permissions to manage resources.
- **Azure Container Registry (ACR):** To store and manage your Docker images. You need to create and configure an ACR instance.
- **Azure Container App:** A running Azure Container App to host your deployed FastAPI application.
- **Azure App Registration:** Register your application in Azure Active Directory (Azure AD) to enable authentication for the GitHub Actions workflow.
- **GitHub:** A GitHub repository where your FastAPI code is hosted and where the GitHub Actions workflow will be configured.
