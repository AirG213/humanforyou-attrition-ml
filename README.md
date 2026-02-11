# HumanForYou Attrition ML

Machine Learning project to analyze and predict employee attrition.

## Prerequisites
- Python 3 must be installed on your machine and available in your `PATH`.
- Node.js and npm (optional, for Playwright MCP server integration)

## Installation
1. Create a virtual environment:
   ```powershell
   python -m venv .venv
   ```
2. Activate the virtual environment:
   ```powershell
   .\.venv\Scripts\Activate.ps1
   ```
   Si erreur de sécurité (windows):
   ```powershell
   Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned .\.venv\Scripts\Activate.ps1
   ```  
3. Install dependencies from `requirements.txt`:
   ```powershell
   python -m pip install -r requirements.txt
   ```

## Objective
Identify key drivers of attrition and build predictive models.

## Data Sources
- HR data
- Manager evaluation
- Employee survey
- In/Out working time logs

## GitHub Copilot MCP Server Configuration

This repository includes configuration for the Playwright MCP (Model Context Protocol) server to enhance GitHub Copilot capabilities.

### Setup Instructions

#### Option 1: Use the Copilot CLI (Interactive)
```bash
/mcp add
```

#### Option 2: Manual Configuration
1. Copy the MCP configuration to your Copilot directory:
   ```bash
   mkdir -p ~/.copilot
   cp .copilot/mcp-config.json ~/.copilot/mcp-config.json
   ```

2. Alternatively, manually create or edit `~/.copilot/mcp-config.json` with the following content:
   ```json
   {
     "mcpServers": {
       "playwright": {
         "type": "local",
         "command": "npx",
         "tools": [
           "*"
         ],
         "args": [
           "@playwright/mcp@latest"
         ]
       }
     }
   }
   ```

For more information, see the [Copilot CLI documentation](https://docs.github.com/en/copilot/using-github-copilot/using-github-copilot-in-the-command-line).
