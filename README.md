# vsts-aci-build-agent
An on-demand VSTS build agent running on Azure Container Instances

> Note: Azure DevOps has made a ton of improvements since I came up with this hack. If you want builds that run inside containers at pay-per-minute rates, you should check out [container jobs](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/container-phases?view=azdevops&tabs=yaml) - you still get the isolated environment with whatever you want in it, pay based on usage, but you don't have to wire up a ton of hacks & functions to orchestrate everything
