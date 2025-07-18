**GoREST API Chaining – Postman Collection**(GoRest_ApiChaining.postman_collection.json)
This Postman project demonstrates API chaining using the public GoREST API, where data is passed between requests using Postman environment variables. It simulates a typical user lifecycle:

➡️ Create → Get → Update → Delete

**📌 Features**
Dynamically generates a random username and email for each user.

Captures and stores the user ID from the create response to reuse in subsequent requests.

Demonstrates API chaining using environment variables (username, useremail, id).

Cleans up by deleting the created user and unsetting variables.

**🔄 Request Flow**



**1️⃣ Create User (POST)**
Pre-request script generates a random username and useremail, then sets them as environment variables.

Sends a POST request using those variables in the request body.

On success, extracts the id from the response and stores it as an environment variable (id).

**2️⃣ Get User by ID (GET)**
Uses the stored {{id}} to fetch the created user's details.

**3️⃣ Update User (PUT or PATCH)**
Updates the user details using the same {{id}}.

**4️⃣ Delete User (DELETE)**
Deletes the user by referencing {{id}}.

Post-request script unsets the environment variables to clean up.

**🧪 Environment Variables Used**
Variable	Description
username	Randomly generated user name
useremail	Randomly generated user email
id	ID of the created user from response

**⚙️ How to Use**
Import the Postman collection and the environment file (.postman_environment.json) into Postman.

Set your GoREST API token in the collection-level Authorization tab (Bearer Token).

Ensure all requests inherit auth from the parent.

Run the requests step-by-step or use Collection Runner to execute the full flow.






****Student Data API – Postman Collection with Variable Management****
This Postman project demonstrates testing a custom API built using JSON Server. The API simulates student data operations and explores the usage of different variable scopes in Postman: environment, collection, local, and global.

It covers the complete CRUD operations – Create, Read, Update, and Delete – on student records using data defined in **StudentData.json.**

A custom Student Data API created using json-server via command line.

**A Postman collection (StudentDataVariables.postman_collection.json) to test the API**.

Demonstrates use of local, environment, collection, and global variables.

Proper unset of variables done in the post-request script to maintain clean state.

****🔄 Request Flow**
**Create Student (POST)**
Generates student data and sends a POST request to {{url_collect}}/students

Captures the student id from the response using:

const jsonData = pm.response.json();
pm.environment.set("studentId", jsonData.id);
Stores it in an environment variable for chaining

**2. Get Student by ID (GET)**
Uses {{studentId}} in the request to fetch student details

Verifies the student is created successfully

**3. Update Student (PUT or PATCH)**
Updates the created student using the {{studentId}}

Sends new data and confirms the update via response checks

**4. Delete Student (DELETE)**
Deletes the student using {{studentId}}

Cleans up by unsetting variables in the Post-request script:
pm.environment.unset("studentId");

**🌐 Setting the Base URL**
The API base URL is saved in an environment variable named url_global,url_local,url_collect.

For example:
baseUrl = http://localhost:3000
Then, your requests use:
{{url_global}}/students



**How to create api and collection**

Run json-server with your data file:
json-server StudentData.json

Import the following into Postman:

The StudentDataVariables.postman_collection.json collection

An environment with baseUrl set as http://localhost:3000

Run each request in sequence or automate using the Collection Runner



********************************************************📘 API Testing with Postman + CSV + json-server********************************************************

This project demonstrates data-driven API testing using Postman, a CSV data file, and a mock REST API built with `json-server`. The focus is on creating posts with `title` and `author` fields using parameterization, and testing full CRUD operations.

## 🚀 What This Project Does

- Sends multiple **POST** requests with different titles and authors from `posts_data.csv`
- Uses `json-server` to simulate a REST API (`http://localhost:3000`)
- Validates `GET`, `PUT`, and `DELETE` requests for created posts
  


**Example API Request**
POST **http://localhost:3000/posts**

Request Body (in Postman):

{
  "title": "{{title}}",
  "author": "{{author}}"
}
Sample Response:

{
  "title": "Test Title 1",
  "author": "Ann",
  "id": 1
}
**How to Run**
**1. Start the Mock API Server**
npm install -g json-server
json-server posts_data.csv
**2. Run Collection**
Make sure Postman variables ({{title}}, {{author}}) match the column names in your CSV file.

**🧩 Tested Endpoints**
Method	Endpoint	Purpose
POST	/posts	Create new posts
GET	/posts/:id	Retrieve specific post
PUT	/posts/:id	Update a post
DELETE	/posts/:id	Delete a post
