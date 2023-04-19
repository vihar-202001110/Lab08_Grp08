# Lab Report

**Group**: _08_  
**Lab**: _08_  
**Objective**: _Backend Unit Testing_

---
This code block describes a unit test for a route called **/api/recipe/fetchallrecipes**. The route is expected to fetch all the recipes of a user.
```javascript
describe("POST /api/recipe/fetchallrecipes", () => {
    it("should get all recipes of the user", async () => {
        const token = await supertest(app).post("/api/auth/login").send({
            email: process.env.TEST_EMAIL,
            password: process.env.TEST_PASSWORD,
        });

        const response = await supertest(app)
            .post("/api/recipe/fetchallrecipes")
            .set({
                "Content-Type": "application/json",
                "auth-token": token.body.authToken
            });

        expect(response.statusCode).toBe(200);
        expect(response.body.length).toBeGreaterThan(0);
    });
});
```
The test is written using the Jest testing framework and supertest library for making HTTP requests. The code block contains one test case that checks if the API endpoint returns a valid response.

The test case uses the async/await syntax to make asynchronous calls to the API endpoint. It first logs in the user by sending a POST request to **/api/auth/login** with the user's email and password. The response from this request contains an authentication token that is used to authorize access to the **/api/recipe/fetchallrecipes** endpoint.

The test then sends a POST request to **/api/recipe/fetchallrecipes** with the authentication token in the headers. It expects a 200 status code and that the response body contains an array with at least one recipe.

The purpose of this test is to verify that the API endpoint is functioning correctly and returning the expected data.

```javascript
describe("POST /api/auth/createuser", () => {
    it("it should create a new user and return an authentication token", async () => {
        const user = {
            name: "Test User",
            email: "testuser@example.com",
            password: "testpassword",
            hasPremium: true
         };
      
          const response = await supertest(app).post("/api/auth/createuser").send(user);
      
          expect(response.status).toBe(201);
    })
});
```
This code block describes a unit test for a route called **/api/auth/createuser**. The route is expected to create a new user 

The test is written using the Jest testing framework and supertest library for making HTTP requests. The code block contains one test case that checks if the API endpoint returns a valid response.

The test case uses the async/await syntax to make asynchronous calls to the API endpoint. It sends a POST request to **/api/auth/createuser** with the user's name, email, password and hasPremium. It expects a 201 status code indicating that the user was created successfully

The purpose of this test is to verify that the API endpoint is functioning correctly and creating new users with the expected response.

> 4 more such test-cases are written as an initial testing attempt, making in total 6 test cases, 2 belonging to user authentication, written in *auth.test.js* and 4 belonging to recipe CRUD operations in *recipe.test.js* file in backend. The output of running all the test-cases can be seen as follows

![image](https://user-images.githubusercontent.com/123557378/233163126-f73bd67d-06b7-4bf0-857b-980c3efd3dc0.png)
  
