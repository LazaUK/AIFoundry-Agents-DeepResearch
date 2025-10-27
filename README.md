# Azure AI Foundry Agent Service: Deep Research tool

This repo demonstrates how to use the **Azure AI Foundry Agent Service** with a Deep Research tool, powred by _o3-deep-research_ AI model. You learn how to to integrate a web-based research capability into your AI agentic solutions.

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
You need an **Azure AI Foundry** project with deployments of `o3-deep-research` and `GPT-4o` AI models.

### 1.2 Authentication
The demo uses **Microsoft Entra ID** authentication via `DefaultAzureCredential` from the `azure.identity` package. To enable this, ensure you are authenticated through the Azure CLI (`az login`), by setting up environment variables for a service principal, or by using a managed identity in an Azure environment.

### 1.3 Environment Variables
Configure the following environment variables with your project details:

| Environment Variable                  | Description                                           |
| :------------------------------------ | :---------------------------------------------------- |
| `AZURE_FOUNDRY_PROJECT_ENDPOINT`      | The endpoint URL for your Azure AI Foundry project.   |
| `AZURE_FOUNDRY_BINGSEARCH_CONNECTION` | The connection ID of Grounding with Bing Search.      |
| `AZURE_FOUNDRY_O3DR_DEPLOYMENT`       | The name of your _o3-deep-research_ deployment.       |
| `AZURE_FOUNDRY_GPT40_DEPLOYMENT`      | The name of your _GPT-4o_ deployment.                 |

### 1.4 Required Libraries
Install the necessary Python packages using pip.

``` bash
pip install azure-ai-agents azure-identity
```

***

## Part 2: Agent and Tool Configuration
This section explains how to define the specialised Deep Research tool and configure your AI agent to utilise it for Web-based research.

### 2.1 Deep Research Tool
The **Deep Research tool** uses a dedicated research model (_o3-deep-research_) and requires a Bing Search grounding connection to retrieve live content from the Internet. It's initialised using the _DeepResearchTool_ class.

The key configuration properties are:
- _bing_grounding_connection_id_: The ID of your Bing Search connection,
- _deep_research_model_: The deployment name of the o3-deep-research model.

``` Python
deep_research_tool = DeepResearchTool(
    bing_grounding_connection_id = BING_SEARCH_CONN_ID,
    deep_research_model = O3DR_DEPLOYMENT,
)
```

### 2.2 Agent Creation
The agent uses a large language model (like GPT-4o) to serve as the orchestrator. This orchestrator model decides when to call the Deep Research tool, interprets the resulting research data and generates the final, user-friendly report.

``` Python
agent = agents_client.create_agent(
    model = GPT4O_DEPLOYMENT,
    name = "deep-research-agent",
    instructions = "You are a helpful Agent that assists in researching scientific topics.",
    tools = deep_research_tool.definitions
)
```

***
