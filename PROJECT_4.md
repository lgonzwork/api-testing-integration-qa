# Project 4: Automated Execution Script & CI/CD Pipeline (PowerShell & GitHub Actions)

## Objective
Standardize and automate the API test execution workflow by orchestrating Newman CLI runs through a custom PowerShell automation script (`run-tests.ps1`) for local environments, integrated with a GitHub Actions CI/CD workflow (`.github/workflows/api-tests.yml`) for continuous integration and automated artifact publishing.

## Test Specifications
- **CLI Runner:** Newman CLI (`newman`)
- **Automation Script:** Windows PowerShell / PowerShell Core (`run-tests.ps1`)
- **CI/CD Platform:** GitHub Actions (`.github/workflows/api-tests.yml`)
- **Reporter Package:** `newman-reporter-htmlextra`
- **Customization:** Dedicated output paths (`.\reports`) and custom dashboard title ("API Functional & Security Test Suite").

## Setup Instructions & Project Structure
1. Ensure the workspace contains the exported Postman artifacts: `collection.json` and `environment.json`.
2. Create the PowerShell automation script `run-tests.ps1` in the project root directory.
3. Configure the GitHub Actions workflow file under `.github/workflows/api-tests.yml`.

## PowerShell Automation Script (`run-tests.ps1`)

```powershell
# Set workspace root
$Workspace = Get-Location

# Define output directories and custom report paths
$ReportDir = "$Workspace\reports"
if (-not (Test-Path $ReportDir)) { New-Item -ItemType Directory -Path$ReportDir }

$ReportPath = "$ReportDir\LatestExecutionReport.html"

Write-Host ">>> Executing Automated API Functional & Security Test Suite..." -ForegroundColor Cyan

# Run Newman with custom HTML reporter settings
newman run collection.json -e environment.json -r cli,htmlextra --reporter-htmlextra-export $ReportPath --reporter-htmlextra-title "API Functional & Security Test Suite"

if ($LASTEXITCODE -eq 0) {
    Write-Host "`n[PASS] Test execution completed successfully. Report generated at: $ReportPath" -ForegroundColor Green
} else {
    Write-Host "`n[FAIL] Test execution encountered failures. Check execution log." -ForegroundColor Red
}

```

## GitHub Actions CI/CD Workflow (.github/workflows/api-tests.yml)

```YAML

name: API Functional & Security Tests

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test-api:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install Newman and Reporters
        run: |
          npm install -g newman
          npm install -g newman-reporter-htmlextra

      - name: Run API Test Suite
        run: |
          newman run collection.json -e environment.json -r cli,htmlextra --reporter-htmlextra-export reports/LatestExecutionReport.html --reporter-htmlextra-title "API Functional & Security Test Suite"

      - name: Upload HTML Test Report Artifact
        uses: actions/upload-artifact@v3
        with:
          name: api-test-report
          path: reports/LatestExecutionReport.html

```

# Expected Test Results

## Local PowerShell Execution: Executing 

```powershell

.\run-tests.ps1

```

Runs the collection headlessly via Newman, renders real-time terminal output, and logs a green success message upon completion.

## HTML Report Customization: 
Generates an interactive audit dashboard saved at .\reports\LatestExecutionReport.html featuring the custom header "API Functional & Security Test Suite".

## CI/CD Pipeline Status: 
Automated push events trigger continuous execution on Ubuntu runners, archiving the generated HTML report as a build artifact in GitHub Actions.
