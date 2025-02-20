### API Endpoint: Refresh Authentication Token

#### **URL**: `/api/user/refresh_token`

#### **Method**: `GET`

#### **Authentication**: Public (Token required)

#### **Description**:
This endpoint allows users to refresh their authentication token. By providing a valid token, the user will receive a new token, and the old token will be invalidated.

---

#### **Request Parameters**:
| Parameter | Type   | Required | Description                                   |
|-----------|--------|----------|-----------------------------------------------|
| `token`   | String | Yes      | The current valid authentication token.       |

---

#### **Example Request**:
```
GET http://localhost:8069/api/user/refresh_token?token=24e635ff9cc74429bed3d420243f5aa6
```

---

#### **Response**:
- **On Success (HTTP 200)**:
  Returns the new authentication token.
  ```json
  {
      "token": "6656a5ba22ca440ca53fd40caeea38eb"
  }
  ```

- **On Failure (HTTP 401)**:
  Returns an error message if the provided token is invalid or not found.
  ```json
  {
      "error": "Invalid User Token"
  }
  ```

- **On Error (HTTP 500)**:
  Returns an error message if an exception occurs during the token refresh process.
  ```json
  {
      "error": " <error_message>"
  }
  ```