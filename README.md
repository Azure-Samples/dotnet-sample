---
page_type: sample
description: "Deploy dotnet application using GitHub Actions"
products:
- GitHub Actions
- Azure App service
languages:
- dotnet
---

# Sample ASP.NET Core application for GitHub Actions

For all samples to set up GitHub workflows, see [Create your first workflow](https://github.com/Azure/actions-workflow-samples

# Steps to create an End-to-End CI/CD Workflow

## Pre-requisites
* Create a new Web App in Azure Portal with runtime stack as .NET and OS as Windows
* Copy Publish Profile Settings of the app

### Create an ASP.NET App Service in Azure

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-webapp-windows-ASPNET%2Fazuredeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-webapp-windows-ASPNET%2Fazuredeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.png"/>
</a>

This template deploys a web app with ASP.NET support. The web app with ASP.NET is an app service that allows you to deploy your ASP.NET website. This will deploy a free tier Windows App Service Plan where you will host your App Service.

If you are new to Azure App Service, see:

- [Azure App Service](https://azure.microsoft.com/services/app-service/web/)
- [Template reference](https://docs.microsoft.com/azure/templates/microsoft.web/allversions)
- [Quickstart templates](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Compute&pageNumber=1&sort=Popular&term=web+apps)

## Configure secrets in the GH repo:
* In the GH repo with Application code, [Define a new secret](https://github.com/Azure/actions-workflow-samples/blob/master/assets/create-secrets-for-GitHub-workflows.md) under repository by navigating to **settings** > **secrets** > **Add a new secret** 
* Paste the contents for the downloaded publish profile file into the secret's value field
* Now in the workflow file in your branch: `.github/workflows/workflow.yml` replace the secret for the input `publish-profile:` of the deploy Azure WebApp action

## test your workflow
* Commit a change in the app code. 
* You should see a new GitHub Action initiated in **Actions** tab.
* At the end of the execution, navigate to the App URL to visualise the change introduced.

## Workflow YAML explained

* [Checkout](https://github.com/actions/checkout) Checks out your Git repository content into Github Actions agent.
* Environment setup using [Setup MSBuild](https://github.com/microsoft/setup-msbuild) - Sets up a ms-build environment by optionally downloading and caching a version of dotnet by SDK version and adding to PATH .
* DotNet Build & Publish
* Deploy to App service using azure/webapps-deploy@v1 action which authenticates using [Azure Web App Publish Profile](https://github.com/projectkudu/kudu/wiki/Deployment-credentials#site-credentials-aka-publish-profile-credentials)
which we configured using the secret set up at the repo level

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
