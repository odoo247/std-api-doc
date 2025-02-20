### API Endpoint: Delete Authentication Token

#### **URL**: `/api/user/delete_token`

#### **Method**: `GET`

#### **Authentication**: Public (Token required)

#### **Description**:
This endpoint allows users to delete their authentication token. After calling this endpoint, the provided token will no longer be valid for future API requests.

---

#### **Request Parameters**:
| Parameter | Type   | Required | Description                                   |
|-----------|--------|----------|-----------------------------------------------|
| `token`   | String | Yes      | The authentication token to be deleted.      |

---

#### **Example Request**:
```
GET http://localhost:8069/api/user/delete_token?token=24e635ff9cc74429bed3d420243f5aa6
```

---

#### **Response**:
- **On Success (HTTP 200)**:
  Returns a success message indicating the token has been deleted.
  ```json
  {
      "success": "Token '24e635ff9cc74429bed3d420243f5aa6' Deleted Successfully"
  }
  ```

- **On Failure (HTTP 404)**:
  Returns an error message if the token is invalid or not found.
  ```json
  {
      "error": "Invalid User Token"
  }
  ```

- **On Error (HTTP 500)**:
  Returns an error message if an exception occurs while deleting the token.
  ```json
  {
      "error": " <error_message>"
  }
  ```