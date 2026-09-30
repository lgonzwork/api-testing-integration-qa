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

```powershell
newman run collection.json -e environment.json -r "cli,htmlextra"; Start-Process (Get-ChildItem .\newman\*.html | Sort-Object CreationTime -Descending | Select-Object -First 1).FullName
```

## Expected Test Results
Terminal Summary Table: Newman displays an in-console summary table logging 3 total requests, 3 test scripts, and 6 passed assertions with 0 failures.

## Interactive Audit Report: 
An HTML file is auto-generated inside the .\newman\ folder featuring a high-level execution dashboard (Newman Run Dashboard), total run duration, data received metrics, and detailed pass/fail status per endpoint.



<img width="1097" height="1007" alt="gitfolioapi_image3" src="https://github.com/user-attachments/assets/d840e96f-055a-4487-8d9c-c73307954861" />


<img width="1890" height="930" alt="gitfolioapi_image4" src="https://github.com/user-attachments/assets/22df3203-d539-47e8-88ae-1c8d06b9a520" />


<img width="1893" height="961" alt="gitfolioapi_image5" src="https://github.com/user-attachments/assets/4503ee45-0449-4159-b869-a89b78a9c978" />


<img width="1887" height="962" alt="gitfolioapi_image6" src="https://github.com/user-attachments/assets/37e43c93-7b09-4543-977b-32b52d52d623" />




