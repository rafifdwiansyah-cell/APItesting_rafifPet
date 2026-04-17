📌 API Testing - Petstore (Postman + Newman)

Automation API Testing menggunakan Postman Collection + Newman CLI untuk Swagger Petstore API.

🚀 Tech Stack
Postman
Newman
JavaScript (Postman Tests)
Swagger Petstore API
📂 Collection Overview

Collection ini mencakup:

CRUD Pet (Create, Read, Update, Delete)
Order Management
Positive & Negative Test Cases
Environment Variable chaining (petId, orderId)
Assertions using Postman Tests
🌐 Base URL
https://petstore.swagger.io/v2
📌 Test Coverage
🟢 Positive Test Cases
Create Pet
Get Pet by ID
Update Pet
Delete Pet
Create Order
Get Order by ID
🔴 Negative Test Cases
GET invalid Pet ID
GET invalid Order ID
POST empty payload /pet
PUT invalid pet ID
DELETE invalid pet
Invalid status query
Upload image invalid pet
POST invalid order payload
🔗 Chaining Concept

Collection menggunakan environment variables:

Variable	Description
petId	ID pet dari Create Pet
orderId	ID order dari Create Order

Contoh:

pm.environment.set("petId", jsonData.id);
✅ Assertions Example
Status Code Check
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
Dynamic ID Validation
pm.test("Pet ID match", function () {
    pm.expect(jsonData.id).to.eql(parseInt(pm.environment.get("petId")));
});
⚠️ Negative Testing Strategy

Karena Swagger Petstore tidak konsisten, negative test dibuat flexible:

pm.expect([200, 400, 404, 405, 500]).to.include(pm.response.code);

👉 Ini memastikan test tidak flaky (tidak mudah FAIL karena API tidak stabil).

🛠️ How to Run (Newman)
1. Install Newman
npm install -g newman
2. Install HTML Reporter
npm install -g newman-reporter-htmlextra
3. Run Collection
newman run rafifPetstore_API.json -r cli,htmlextra
4. Generate HTML Report
newman run rafifPetstore_API.json -r htmlextra --reporter-htmlextra-export report.html
📊 Sample Report Output
HTML Report (interactive)
CLI summary
Test result per request
Response time analysis
📁 Project Structure
APItesting_rafifPet/
│
├── rafifPetstore_API.json
├── report.html
└── README.md
💡 Key Learning
API automation using Postman
Data chaining with environment variables
Positive vs Negative testing strategy
Handling unstable API responses
Newman CLI reporting
Scenario bisa dilihat pada file excel : scenario API rafifPet.xlsx
