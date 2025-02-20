### API Endpoint: Get Authentication Token

#### **URL**: `/api/user/get_token`

#### **Method**: `GET`

#### **Authentication**: Public (No token required)

#### **Description**:
This endpoint allows users to authenticate by providing their login credentials (`login` and `password`). Upon successful authentication, it returns a token that must be used to access other APIs. The token is specific to the authenticated user.

---

#### **Request Parameters**:
| Parameter | Type   | Required | Description                         |
|-----------|--------|----------|-------------------------------------|
| `login`   | String | Yes      | The username of the user.          |
| `password`| String | Yes      | The password associated with the login. |

---

#### **Example Request**:
```
GET http://localhost:8069/api/user/get_token?login=admin&password=admin
```

---

#### **Response**:
- **On Success (HTTP 200)**:
  Returns the authentication token for the user.
  ```json
  {
      "token": "<user_access_token>"
  }
  ```

- **On Failure (HTTP 401)**:
  Returns an error message indicating that the login credentials are incorrect.
  ```json
  {
      "error": "Wrong login/password"
  }
  ```