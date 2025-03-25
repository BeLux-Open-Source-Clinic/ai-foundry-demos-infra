# Azure AI Foundry Demos for Infra

## Description
A brief description of what the project does and its purpose.

## Table of Contents
- Prerequisites
- Installation
- Usage
- Contributing
- License
- Contact

### 📦 Prerequisites    

Before starting the workshop, ensure you have:

- [Python 3.10](https://www.python.org/downloads/) or higher installed
- An active Azure subscription with access to [Azure AI Foundry](https://ai.azure.com)
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) installed
- [Git](https://git-scm.com/downloads) installed
- [VS Code](https://code.visualstudio.com/), [GitHub Codespaces](https://github.com/features/codespaces), or [Jupyter Notebook](https://jupyter.org/install) environment
- Basic Python programming knowledge
- Model deployment and [AI Search](https://learn.microsoft.com/en-us/azure/search/search-what-is-azure-search) connection configured in Azure AI Foundry

---
### Installation
Instructions on how to install and set up the project locally.
```bash
# Clone the repository
git clone https://github.com/BeLux-Open-Source-Clinic/ai-foundry-demos-infra.git

# Navigate to the project directory
cd ai-foundry-demos-infra
```

**Install uv**:
   ```bash
   # Unix/Linux/macOS
   curl -LsSf https://astral.sh/uv/install.sh | sh

   # Windows (PowerShell)
   (Invoke-WebRequest -Uri https://astral.sh/uv/install.ps1 -UseBasicParsing).Content | pwsh
   ```

**Create & activate a virtual environment**:
   ```bash
   uv venv
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
   ```

**Set up Azure AI Foundry**:
   a. **Create Project and Deploy Resources**:
      1. Go to [Azure AI Foundry](https://ai.azure.com)
      2. Create a new AI Hub and Project using the AI Foundry Wizard
      3. Deploy required models:
         - GPT models(gpt-4o, gpt-4o-mini) for chat/completion (**set TPM to max** to avoid issues with Agents notebooks)
         - Embedding model for vector search
         - Ensure the model is deployed in `Global-Standard` or `DataZone-Standard`
      4. Set up connections:
         - Configure [Grounding with Bing](https://learn.microsoft.com/en-us/azure/ai-services/agents/how-to/tools/bing-grounding?view=azure-python-preview&tabs=python&pivots=overview) connection
         - Configure Azure AI Search connection
      5. Add your user account to the `Azure AI Developer` role from Azure AI Foundry Management Portal

   b. **Configure Environment Variables**:
      ```bash
      cp .env.example .env
      ```
      Update `.env` with your Azure AI Foundry values:
      - `PROJECT_CONNECTION_STRING`: Your project connection string from Azure ML workspace
      - `MODEL_DEPLOYMENT_NAME`: Your model deployment name
      - `EMBEDDING_MODEL_DEPLOYMENT_NAME`: Your embedding model deployment name
      - `TENANT_ID`: Your tenant ID from Azure portal
      - `BING_CONNECTION_NAME`: Your Bing search connection name
      - `SERVERLESS_MODEL_NAME`: Your serverless model name


> **Note**: The model specified in `MODEL_DEPLOYMENT_NAME` must be supported by Azure AI Agents Service or Assistants API.
See [supported models](https://learn.microsoft.com/en-us/azure/ai-services/agents/concepts/model-region-support?tabs=python#azure-openai-models) for details.
For Grounding with Bing Search, you need to use `gpt-4o` model.


### Usage

**Install dependencies**:
  ```bash
     # Install core Azure AI SDKs and Jupyter requirements
     uv pip install azure-identity azure-ai-projects azure-ai-inference[opentelemetry] azure-search-documents azure-ai-evaluation azure-monitor-opentelemetry
  
     # Install Jupyter requirements
     uv pip install ipykernel jupyterlab notebook
  
     # Register the kernel with Jupyter
     python -m ipykernel install --user --name=.venv --display-name="Python (.venv)"
  
     # Install additional requirements (optional - for deploying repo or running mkdocs)
     uv pip install -r requirements.txt
  ```

> **Note**: If you encounter kernel errors in VS Code, try:
> 1. Select kernel: Click "Select Kernel" > "Python Environments" > "Python (.venv)"
> 2. If kernel is not listed, run `python -m ipykernel install --user --name=.venv` again, or use the "Create New Kernel" wizard in VS Code to create a new Python environment
> 3. Reload VS Code if needed

**Choose your notebook environment**:

   **Option A: VS Code**
   - Install [VS Code Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
   - Install either:
     - [Jupyter extension](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) for .ipynb files
     - [Polyglot Notebooks extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode) for .dib files
   - Open any notebook and select your Python kernel (.venv)

   **Option B: GitHub Codespaces**
   - Click "Code" > "Create codespace" on the repository
   - Wait for environment setup
   - Notebooks will be ready to run

   **Option C: Jupyter Lab/Notebook**
   ```bash
   # Install Jupyter if you haven't already
   uv pip install jupyterlab notebook

   # Start Jupyter Lab (recommended)
   jupyter lab

   # Or start Jupyter Notebook
   jupyter notebook
   ```
### Contributing

1. Fork the repository. (optional)
2. Create a new branch (git checkout -b feature-branch).
3. Make your changes.
4. Commit your changes (git commit -m 'Add some feature').
5. Push to the branch (git push origin feature-branch).
6. Open a pull request.

### License
This project is licensed under the MIT License.
### Contact
Your Name - jachahbar@microsoft.com

Project Link: https://github.com/BeLux-Open-Source-Clinic/ai-foundry-demos-infra
