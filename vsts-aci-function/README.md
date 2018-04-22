# vsts-aci-function

## StartVSTSBuildAgent / StopVSTSBuildAgent

Creates or destroys an Azure Container Instance that runs the VSTS Build Agent

* Dockerfile is in the `vsts-build-agent-from-scratch` folder
* Creates Container Groups in the `vsts` Resource Group
* You'll need to provide AppSettings in your Function App for `VSTS_AGENT_INPUT_URL` and `VSTS_AGENT_INPUT_TOKEN`
* Places VSTS agents in a pool named `AzureContainerInstance`
* Uses a Service Principal as the other Functions to interact with your Azure Subscription

### Usage

1. Create a `vsts` Resource Group to hold your build agent containers

2. Create a [Function App](https://docs.microsoft.com/en-us/azure/azure-functions/) in Azure

3. Create a Service Principal to be used with the function

```bash
# Create a Service Principal
az ad sp create-for-rbac -n vsts-aci-function
```

4. Set the following App Settings on your function

From VSTS:

* VSTS_AGENT_INPUT_URL
* VSTS_AGENT_INPUT_TOKEN

From your Service Principal:

* TenantId
* ClientId
* ClientSecret

5. Publish the function to Azure

* Open `vsts-aci-function.sln` in VS2017
* Right-click the `Functions` project
* Hit `Publish` and select your your function app