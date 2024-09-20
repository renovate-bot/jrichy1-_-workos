# README

 
Azure Continuous Integration and Deployment (CI/CD) Workflow for Node.js Applications

This workflow automates building, testing, and deploying your Node.js application to an Azure Web App upon code changes pushed to your designated branch ("base" in this example).

Prerequisites:

An existing Azure Web App:
Follow the instructions here to create one: https://docs.microsoft.com/en-us/azure/app-service/quickstart-nodejs?tabs=linux&pivots=development-environment-cli   
A GitHub repository containing your Node.js application code.
Configuration:

Azure Web App Publish Profile:

Download the Publish Profile file from your Azure Web App's Overview page in the Azure Portal.
Create a secret named AZURE_WEBAPP_PUBLISH_PROFILE in your GitHub repository settings, storing the publish profile content as the secret's value.
Reference: https://docs.microsoft.com/en-us/azure/app-service/deploy-github-actions?tabs=applevel#generate-deployment-credentials   
Environment Variables:

Update the following environment variables in the .github/workflows/nodejs-azure-deploy.yml file as needed:
AZURE_WEBAPP_NAME: Set to your application's name in Azure.
AZURE_WEBAPP_PACKAGE_PATH (optional): Change the path to your project directory within the repository (defaults to the root).
NODE_VERSION (optional): Specify the desired Node.js version.
Workflow Steps:

Trigger:

The workflow runs upon code pushes to the "base" branch or a manual trigger.
Build Job:

Runs on an Ubuntu-based runner.
Checks out your repository code.
Sets up the specified Node.js version using the actions/setup-node@v4 action.
Executes npm install to download dependencies.
Optionally runs npm run build and npm run test scripts if defined in your project.
Uploads the built artifacts (presumably your application code) for the deployment job.
Deployment Job:

Runs on an Ubuntu-based runner, triggered by the successful build job.
Downloads the uploaded build artifacts.
Deploys the application to your Azure Web App using the azure/webapps-deploy@v3 action.
Provides the deployment URL as an output for environment variable access in subsequent steps or workflows (optional).
Additional Notes:

Consider using a version control system like Git for managing changes to your code and workflow file.
Explore other features of GitHub Actions, such as environment variables inheritance and matrix builds, for further customization.
Securely store sensitive information like the publish profile within GitHub secrets.
Refer to the provided documentation for more details on the actions and steps involved.
Resources:

GitHub Actions for Azure: https://github.com/Azure/Actions
Azure Web Apps Deploy action: https://github.com/Azure/webapps-deploy
GitHub Actions workflow samples for Azure deployments: https://github.com/Azure/actions-workflow-samples
