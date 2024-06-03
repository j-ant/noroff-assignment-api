# Noroff Assignment API

The Noroff Assignment API will be used to complete assignments where a personal API is required.

## Prerequisites
In order to use the API you will require the following:
1. A [GitHub](https://github.com/) account.
2. A [Glitch](https://glitch.com/) account.

## Instructions
Follow the instructions below to get your API setup and ready for use.

1. Fork this repository to your GitHub account.
2. Create a new project on Glitch and link the forked repository from GitHub.
3. Add two environment variables to the project, `NODE_ENV` and `API_KEY`.
   - Assign the value `prod` to `NODE_ENV`.
   - Generate a random 64-character string. Assign this string to `API_KEY`. Keep this value a **secret**, it should not be publicly visible anywhere in your project. You will use this value in your front-end application to send some API requests to protected endpoints.
4. Glitch will generate a random slug for your project, e.g., "wonderful-frosty-jumper". To test that your API is live, navigate to `https://<glitch-project-slug>.glitch.me`.

## Accessing Endpoints

Each API endpoint contains both open and protected endpoints. All `GET` endpoints are open. Any other methods `POST`, `PUT`, `PATCH` and `DELETE` are protected with the `X-API-KEY` header.

## Endpoints

**`GET`** /users
**`GET`** /users?username=<query>

### Sample Code
```javascript
const API_URL = 'your-api-url' // Step 4 of the instructions above
const username = 'harry_houdini'

fetch(`${API_URL}/users?username=${username}`)
    .then(response => response.json())
    .then(results => {
        // results will be an array of users that match the username of 'harry_houdini'.
    })
    .catch(error => {
    })
```

## Protected Endpoints

Protected endpoints require `X-API-Key` attached to the request header with the API key as the value.

🔒 **`POST`** /users
The POST method is used to add a new record.

### Sample Code
```javascript
const API_URL = 'your-api-url' // Step 4 of the instructions above
const apiKey = 'your-api-key' // Step 3 of the instructions above

fetch(`${API_URL}/users`, {
        method: 'POST',
        headers: {
          'X-API-Key': apiKey,
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ 
            username: 'new_user1337', 
            favourites: [] 
        })
    })
    .then(response => {
      if (!response.ok) {
        throw new Error('Could not create new user')
      }
      return response.json()
    })
    .then(newUser => {
      // newUser is the new user with an id
    })
    .catch(error => {
    })
```

### Sample Response

```json
{
    "id": 2,
    "username": "new_user1337",
    "favourites": []
}
```
🔒 **`PATCH`** /users/{:id}
The PATCH method is used to update a single record.

### Sample Code
```javascript
const API_URL = 'your-api-url' // Step 4 of the instructions above
const apiKey = 'your-api-key' // Step 3 of the instructions above
const userId = 1 // Update the user with id 1

fetch(`${API_URL}/users/${userId}`, {
        method: 'PATCH',
        headers: {
          'X-API-Key': apiKey,
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ 
            // Provide new favourites to add to user with id 1
            favourites: ["item 1", "item 2", "item 3"] 
        })
    })
    .then(response => {
      if (!response.ok) {
        throw new Error('Could not update user favourites')
      }
      return response.json()
    })
    .then(updatedUser => {
      // updatedUser is the updated user with the patched data
    })
    .catch(error => {
    })
```

# Special thanks to Typicode for json-server

[GitHub: json-server](https://github.com/typicode/json-server)
