# HumanForYou Attrition ML

Machine Learning project to analyze and predict employee attrition.

## Prerequisites
- Python 3 must be installed on your machine and available in your `PATH`.

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
