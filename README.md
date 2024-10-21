# Azure-ContainerApp-Continuous-Deployment-Using-GitHub-Actions

**In this, I will take you through setting up a GitHub Actions workflow for continuous deployment of a FastAPI application using Docker and Azure Container Apps. FastAPI is a modern web framework known for its high performance and ease of use. In this scenario, we will automate the process of logging into your Azure account, building the FastAPI app into a Docker image, pushing the image to Azure Container Registry (ACR), and deploying the container to Azure Container Apps. This solution ensures seamless continuous deployment, automatically updating your application with each new commit, offering both scalability and agility for modern cloud-native applications.**
Here is a simple flow chart:

```mermaid
graph TD;
    graph TD;
    Developer-->GitHub;
    GitHub-->Runs_GitHub_Workflow_File;
    Runs_GitHub_Workflow_File-->Azure_Login;
    Azure_Login-->Image_pushed_to_ACR;
    Image_pushed_to_ACR-->Update_Container_App_Deployment;
```
