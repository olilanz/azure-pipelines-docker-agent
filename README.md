# azure-pipelines-docker-agent
Self-hosted Azure Pipelines Agent in Docker

Runs a build agent on your own hardware. Useful if either your source code or your deplyment environments are hosted in private infrastructure, but you still want to power of automation of Azure DevOps.

Based on Microsoft docs: https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops

## Build and run

```
docker build -t dockeragent:latest .
docker run -e AZP_URL=<Azure DevOps instance> -e AZP_TOKEN=<PAT token> -e AZP_AGENT_NAME=mydockeragent dockeragent:latest --once
```

## Environment variables

- AZP_URL:	The URL of the Azure DevOps or Azure DevOps Server instance.
- AZP_TOKEN:	Personal Access Token (PAT) with Agent Pools (read, manage) scope, created by a user who has permission to configure agents, at AZP_URL.
- AZP_AGENT_NAME:	Agent name (default value: the container hostname).
- AZP_POOL:	Agent pool name (default value: Default).
- AZP_WORK:	Work directory (default value: _work).

## Docker in Docker

For supporting build jobs that require access to a Docker Engine, you will need to mount the Docker socket into the container, and run the container in privileged mode. This will give the build agent full access to Dcoker Engine. 

Not that this elevates the agent to run as root, which may have severe security implications. Do this only in environments and configurations you trust.
