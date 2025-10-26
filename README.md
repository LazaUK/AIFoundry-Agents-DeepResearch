# Azure AI Foundry Agent Service: Deep Research tool

This repo demonstrates how to use the **Azure AI Foundry Agent Service** with a Deep Research tool, powred by _o3-deep-research_ AI model. You learn how to to integrate a web-based research capability into your Ai agentic solutions.

> [!NOTE]
> For detailed information about the Azure AI Foundry Agent Service's Deep Research tool, refer to the official [Azure AI Foundry documentation](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/tools/deep-research).

***

## 📑 Table of Contents:
- [Part 1: Configuring the Environment](#part-1-configuring-the-environment)
- [Part 2: ]()
- [Part 3: ]()

## Part 1: Configuring the Environment
To run the provided Jupyter notebook, you'll need to set up your Azure AI Foundry environment and install the required Python packages.

### 1.1 Prerequisites
You need an **Azure AI Foundry** project with a deployment of `o3-deep-research` AI model.

### 1.2 Authentication
The demo uses **Microsoft Entra ID** authentication via `DefaultAzureCredential` from the `azure.identity` package. To enable this, ensure you are authenticated through the Azure CLI (`az login`), by setting up environment variables for a service principal, or by using a managed identity in an Azure environment.

### 1.3 Environment Variables
Configure the following environment variables with your project details:

| Environment Variable             | Description                                           |
| :------------------------------- | :---------------------------------------------------- |
| `AZURE_FOUNDRY_PROJECT_ENDPOINT` | The endpoint URL for your Azure AI Foundry project.   |
| `AZURE_FOUNDRY_GPT_MODEL`        | The name of your o3-deep-research model's deployment. |

### 1.4 Required Libraries
Install the necessary Python packages using pip.

``` bash
pip install azure-ai-agents azure-identity
```

***

## Part 2: Agent and Tool Configuration
