**Trello API Test Collection**
This repository contains a collection of tests for the Trello API, created using Postman. The test suite focuses on the Happy Path for managing Trello boards, lists, and cards, ensuring that core functionalities are working as expected.

**Overview**
The test suite consists of several API requests that cover common Trello operations. Each request includes assertions to validate that the API responses meet expected outcomes. These tests can be executed through Postman or integrated into a CI/CD pipeline for automated validation.

**Base URL**
The base URL for all Trello API requests is: https://api.trello.com/

**API Tests Included**

**1. Create a Board**
Description: This test creates a new Trello board with the specified name.
Method: POST
Assertions: 
  Status code is 200.
  The board is successfully created with the correct name.
  The board is private.
  The calendar view is disabled.

   **javascript**
    pm.test("Status code is 200", function () {
        pm.response.to.have.status(200);
    });
    pm.test('Board is created', () => {
        pm.expect(response.name).to.eql('4 Board');
        pm.expect(response.closed).to.be.false;
    });
    pm.test('Board is private', () => {
        pm.expect(response.prefs.permissionLevel).to.eql('private');
    });
    pm.test('Calendar is disabled', () => {
        pm.expect(calendarView.enabled).to.be.false;
    });

**2. Get All Boards**
Description: Fetches all the boards associated with the user's account.
Method: GET
Assertions: Status code is 200.
    **javascript**
    pm.test("Status code is 200", function () {
        pm.response.to.have.status(200);
    });

**3. Get a Single Board**
Description: Retrieves details of a specific board using its ID.
Method: GET
Assertions: Status code is 200.
   
   **javascript**
  pm.test("Status code is 200", function () {
      pm.response.to.have.status(200);
  });

**4. Create a "To Do" List in a Board**
Description: Creates a new list named "TODO" in an existing board.
Method: POST
Assertions:
  Status code is 200.
  The list is created with the correct name.
  The list is part of the correct board.

  **javascript**
  pm.test("Status code is 200", function () {
      pm.response.to.have.status(200);
  });
  pm.test('TODO list is created', () => {
      pm.expect(response.name).to.eql('TODO');
      pm.expect(response.idBoard).to.eql(pm.collectionVariables.get('boardId'));
  });

**5. Create a "Done" List in a Board**
Description: Creates a "DONE" list in the board.
Method: POST
Assertions:
  Status code is 200.
  The "DONE" list is successfully created.
  
**6. Create a Card in the "To Do" List**
Description: Adds a new card to the "TODO" list within the board.
Method: POST
Assertions:
  Status code is 200.
  The card is created in the correct list and board.
  
**7. Move a Card to the "Done" List**
Description: Moves an existing card from the "TODO" list to the "DONE" list.
Method: PUT
Assertions:
  The card is successfully moved to the "DONE" list.
  
**8. Delete a Board**
Description: Deletes an existing board.
Method: DELETE
Assertions:
  Status code is 200.
  The board is successfully deleted.
  
**9. Get Deleted Board**
Description: Attempts to retrieve a deleted board, expecting a 404 error.
Method: GET
Assertions: Status code is 404.


**Environment Variables**
To run the tests, the following environment variables are required:

  baseUrl: Base URL for the Trello API.
  Key: Your Trello API key.
  Token: Your Trello API token.
  boardId: The ID of the board created during the tests.
  These variables can be configured in Postman or passed via the environment.

**How to Run the Tests**
1.Clone this repository.
2.Import the Postman collection into your Postman application.
3.Set up your environment variables (Key, Token, etc.).
4.Run the tests manually or through Postman’s collection runner.

**License**
This project is licensed under the MIT License - see the LICENSE file for details.
