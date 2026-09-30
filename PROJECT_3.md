# Project 3: Headless Execution & HTML Reporting via Newman CLI

## Objective
Decouple API test execution from the Postman desktop GUI by orchestrating collection runs through the Newman command-line interface, automatically generating interactive HTML audit reports for test execution analysis.

## Test Specifications
- **CLI Runner:** Newman CLI (`newman`)
- **Reporter Package:** `newman-reporter-htmlextra`
- **Environment Target:** `LAB_Environment` (`environment.json`)
- **Scope:** Automated execution of functional assertions, environment variable persistency checks, and HTML dashboard rendering.

## Setup Instructions & Execution Command
1. Open PowerShell and navigate to the project directory containing the exported artifacts (`collection.json` and `environment.json`).
2. Run the collection headlessly with double reporters (`cli` for real-time terminal output and `htmlextra` for dashboard generation):

```powershell
newman run collection.json -e environment.json -r cli,htmlextra
```
Optionally, execute and auto-open the latest generated HTML report in the default browser:
newman run collection.json -e environment.json -r "cli,htmlextra"; Start-Process (Get-ChildItem .\newman\*.html | Sort-Object CreationTime -Descending | Select-Object -First 1).FullName

Expected Test Results
Terminal Summary Table: Newman displays an in-console summary table logging 3 total requests, 3 test scripts, and 6 passed assertions with 0 failures.

Interactive Audit Report: An HTML file is auto-generated inside the .\newman\ folder featuring a high-level execution dashboard (Newman Run Dashboard), total run duration, data received metrics, and detailed pass/fail status per endpoint.
