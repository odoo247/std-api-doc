### API Endpoint: Search Records in a Model

#### **URL**:  
1. `/api/<string:model>/search`  
2. `/api/<string:model>/search/<int:id>`  

#### **Method**: `GET`

#### **Authentication**: Public (Token required)

#### **Description**:  
This endpoint allows users to retrieve records from a specific Odoo model.  
- If an ID is provided in the URL, the endpoint returns the record matching the ID.  
- If a domain is provided in the query parameters, it filters records based on the domain.  
- If neither is provided, it returns all records with their `id` and `name` fields.  
The results can be further filtered using `fields`, `offset`, and `limit` parameters.

---

#### **Request Parameters**:
| Parameter  | Type    | Required | Description                                                                                           |
|------------|---------|----------|-------------------------------------------------------------------------------------------------------|
| `model`    | String  | Yes      | The name of the Odoo model (e.g., `res.partner`, `sale.order`).                                       |
| `id`       | Int     | No       | The specific record ID to retrieve.                                                                  |
| `token`    | String  | Yes      | The authentication token of the user.                                                                |
| `domain`   | List    | No       | A JSON-formatted domain for filtering records (e.g., `[('id', '>=', 7)]`).                           |
| `fields`   | List    | No       | A list of field names to retrieve in the response (e.g., `['name', 'email']`). Defaults to `id` and `name`. |
| `offset`   | Int     | No       | The starting index for the result set (used for pagination). Default is `0`.                         |
| `limit`    | Int     | No       | The maximum number of records to return. Defaults to no limit.                                       |

---

#### **Example Requests**:

1. **Retrieve a Single Record by ID**  
   URL:  
   ```
   GET http://localhost:8069/api/res.partner/search/1?token=24e635ff9cc74429bed3d420243f5aa6
   ```  
   **Response**:
   ```json
   [
       {
           "id": 1,
           "name": "John Doe"
       }
   ]
   ```

2. **Search Records Using a Domain with Pagination**  
   URL:  
   ```
   GET http://localhost:8069/api/res.partner/search?token=24e635ff9cc74429bed3d420243f5aa6&domain=[('id', '>=', 7)]&offset=10&limit=5
   ```  
   **Response**:
   ```json
   [
       {
           "id": 7,
           "name": "Jane Smith"
       },
       {
           "id": 8,
           "name": "Alice Johnson"
       }
   ]
   ```

3. **Retrieve Specific Fields**  
   URL:  
   ```
   GET http://localhost:8069/api/res.partner/search?token=24e635ff9cc74429bed3d420243f5aa6&fields=['name','email']
   ```  
   **Response**:
   ```json
   [
       {
           "id": 1,
           "name": "John Doe",
           "email": "john.doe@example.com"
       },
       {
           "id": 2,
           "name": "Jane Smith",
           "email": "jane.smith@example.com"
       }
   ]
   ```

---

#### **Response**:
- **On Success (HTTP 200)**:  
  Returns a list of records matching the conditions. Each record includes the `id` field and any other requested fields.  

- **On Failure (HTTP 401)**:  
  If the user token is invalid:  
  ```json
  {
      "error": "Invalid User Token"
  }
  ```

- **On Failure (HTTP 400 or 500)**:  
  If the model is not found or an exception occurs:  
  ```json
  {
      "error": "Model Not Found or <error_message>"
  }
  ```

---

#### **Notes**:
1. **Security**: Ensure the user has access rights to view the records in the specified model.
2. **Pagination**: Use the `offset` and `limit` parameters for efficient data retrieval when dealing with large datasets.
3. **Field Customization**: If no `fields` are specified, the default response includes only the `id` and `name` fields. Additional fields must be explicitly requested using the `fields` parameter.
4. **Domain Filtering**: The `domain` parameter should follow Odoo’s domain syntax and must be passed as a JSON string.