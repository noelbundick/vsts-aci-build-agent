# vsts-build-agent

This image contains the [Visual Studio Team Services Build and Release Agent](https://github.com/Microsoft/vsts-agent) for Linux. It also contains some basic support for building Python applications. This is an example of how to build a minimal build agent from scratch.

See [vsts-agent-docker](https://github.com/Microsoft/vsts-agent-docker) for the Docker-based Hosted Linux Agent.

## Usage - Docker

As a thin wrapper over the base scripts, most configuration is done via environment variables. Per the VSTS agent docs, "Any command line argument can be specified as an environment variable. Use the format `VSTS_AGENT_INPUT_<ARGUMENT_NAME>`. For example: `VSTS_AGENT_INPUT_PASSWORD`

> The full list of options can be found by running `config.sh --help`

So an example to run an agent named `docker-0` in an agent pool named `Docker` would look like:

```bash
docker run --rm -it -e VSTS_AGENT_INPUT_URL=https://noelbundick.visualstudio.com -e VSTS_AGENT_INPUT_AUTH=pat -e VSTS_AGENT_INPUT_TOKEN=S4GGVbTQs58h6NbmJBY7cn98CKoyQSC1CSWMmCIx3aMkOhRppLDh -e VSTS_AGENT_INPUT_POOL=Docker -e VSTS_AGENT_INPUT_AGENT=docker-0 vsts-build-agent
```

## Usage - Azure Container Instance

This image can also be used to run a build agent on [Azure Container Instances](https://azure.microsoft.com/en-us/services/container-instances/). An example that runs an agent named `vsts-agent-0` in an agent pool named `AzureContainerInstance` would look like:

```bash
az container create -n vsts-agent-0 -g vsts --cpu 2 --memory 3.5 --image acanthamoeba/vsts-build-agent -e VSTS_AGENT_INPUT_URL=https://noelbundick.visualstudio.com VSTS_AGENT_INPUT_AUTH=pat VSTS_AGENT_INPUT_TOKEN=S4GGVbTQs58h6NbmJBY7cn98CKoyQSC1CSWMmCIx3aMkOhRppLDh VSTS_AGENT_INPUT_POOL=AzureContainerInstance VSTS_AGENT_INPUT_AGENT=vsts-agent-0
```