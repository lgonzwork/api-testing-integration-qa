# Project 2: Dynamic Environment Variables & Data Pass (UI Desktop)

## Objective
Automate multi-request API workflows by dynamically extracting attributes (such as resource IDs or authentication tokens) from an initial HTTP response payload using `pm.environment.set`, and mapping them into subsequent requests using `{{variable_name}}` syntax.

## Test Specifications
- **Request 1 (POST — Create Resource):**
  - **Endpoint:** `https://jsonplaceholder.typicode.com/posts`
  - **Body (raw JSON):** `{"title": "Security Audit Test", "body": "Automated payload", "userId": 1}`
  - **Action:** Extract generated `id` from the response JSON and store it in an environment variable named `created_post_id`.
- **Request 2 (GET — Fetch Resource):**
  - **Endpoint:** `https://jsonplaceholder.typicode.com/posts/1` (simulated via `https://jsonplaceholder.typicode.com/posts/{{created_post_id}}`)
  - **Action:** Pass `{{created_post_id}}` dynamically within the URL path.

## Setup Instructions
1. In your Postman Collection `[LAB] Postman & Newman Master`, add a subfolder named `Project 2 - Dynamic Variables`.
2. Create an active Postman Environment named `LAB_Environment`.
3. Add Request 1 (POST to `https://jsonplaceholder.typicode.com/posts`). In the Body tab, select `raw` -> `JSON` and paste the request body.
4. Navigate to the Scripts (or Tests) tab of Request 1, paste the extraction script below, and click Send.
5. Add Request 2 (GET to `https://jsonplaceholder.typicode.com/posts/{{created_post_id}}`) to verify dynamic parameter injection.

## Test Script (Request 1 — Post-Response Extraction)

```javascript
// Assertion 1: Validate HTTP Status Code 201 Created
pm.test("Status code is 201 Created", function (){
    pm.response.to.have.status(201);
});

// Extract value and set Environment Variable dynamically
var jsonData = pm.response.json();
pm.environment.set("created_post_id", jsonData.id);

// Assertion 2: Verify variable persistence in environment state
pm.test("Environment variable 'created_post_id' set successfully", function (){
    var storedValue = pm.environment.get("created_post_id");
    pm.expect(storedValue).to.eql(jsonData.id);
});
```

## Expected Test Results
- Request 1 Status: 201 Created
- Test Suite Status: 2/2 Passed (PASS)
- Environment State: Variable `created_post_id` populated automatically in `LAB_Environment`.
- Request 2 Execution: URL resolves dynamically to `https://jsonplaceholder.typicode.com/posts/101` (or extracted ID value) without manual entry.



<img width="1919" height="1013" alt="gitfolioapi_image2" src="https://github.com/user-attachments/assets/23187916-6447-473a-b0dd-91e1640609e4" />
