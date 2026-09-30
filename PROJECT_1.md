# Project 1: Functional Assertions & Schema Basics (UI Desktop)

## Objective
Establish baseline API functional testing by configuring HTTP requests within the Postman Desktop UI and applying built-in JavaScript assertions to validate response status codes, headers, and JSON body payload structures.

## Test Specifications
- HTTP Method: GET
- Target Endpoint: https://jsonplaceholder.typicode.com/posts/1
- Scope: Response status validation, header inspection, and payload data type verification.

## Setup Instructions
1. Create a collection named [LAB] Postman & Newman Master.
2. Add a subfolder named Project 1 - Functional Assertions.
3. Create a new GET request pointing to https://jsonplaceholder.typicode.com/posts/1.
4. Navigate to the Scripts (or Tests) tab below the URL bar.
5. Paste the test script below and click Send.

## Test Script
```javascript
// Assertion 1: Validate HTTP Status Code
pm.test("Status code is 200 OK", function (){
    pm.response.to.have.status(200);
});

// Assertion 2: Validate Content-Type Header
pm.test("Header Content-Type includes application/json", function (){
    pm.response.to.have.header("Content-Type");
    pm.expect(pm.response.headers.get("Content-Type")).to.include("application/json");
});

// Assertion 3: Validate JSON Payload Attribute and Type
pm.test("Payload contains a valid numeric ID equal to 1", function (){
    var jsonData = pm.response.json();
    pm.expect(jsonData.id).to.eql(1);
    pm.expect(jsonData.id).to.be.a('number');
});

```
## Expected Test Results
- HTTP Status: 200 OK
- Test Suite Status: 3/3 Passed (PASS)
  - Assertions Evaluated:
    - Status code is 200 OK — PASS
    - Header Content-Type includes application/json — PASS
    - Payload contains a valid numeric ID equal to 1 — PASS
   
      

<img width="1906" height="1016" alt="gitfolioapi_image1" src="https://github.com/user-attachments/assets/f9938324-1927-468d-aa6e-283e7c6b155b" />
