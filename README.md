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

