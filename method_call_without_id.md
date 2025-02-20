### API Endpoint: Call Model Method

#### **URL**: `/api/<string:model>/method/<string:method_name>`

#### **Method**: `GET`

#### **Authentication**: Public (Token required)

#### **Description**:
This endpoint allows users to call methods on specific records of any Odoo model. It supports both positional (`args`) and keyword (`kwargs`) arguments. 

**MODEL**

```sale.order```

**METHOD**

1. ```magento_update_warehouse```
2. ```magento_update_tracking_number```

**ARGUMENTS**
```json
{
    "kwargs": 
    {
        "order_id": "Magento order ID",
        "items": [
            {
              "order_line_id": "Magento order line ID",
              "warehouse_source_code": "Source codes in Magento",
              "tracking_number": "Tracking Number"
             }
        ]
    }
}
```
---

#### **Request Parameters**:
| Parameter      | Type   | Required | Description                                                                                           |
|----------------|--------|----------|-------------------------------------------------------------------------------------------------------|
| `model`        | String | Yes      | The name of the Odoo model (e.g., `sale.order`, `res.partner`).                                       |
| `method_name`  | String | Yes      | The method name to be called on the record.                                                          |
| `token`        | String | Yes      | The authentication token of the user.                                                               |
| `args`         | List   | No       | A JSON-formatted list of positional arguments to pass to the method.                                 |
| `kwargs`       | Dict   | No       | A JSON-formatted dictionary of keyword arguments to pass to the method.                              |

---

#### **Example Requests**:

1. **Calling a Method Without Arguments**  
   URL:  
   ```
   GET http://localhost:8069/api/sale.order/method/action_button_confirm/?token=1ec448c54a004165b4c0da976b227260
   ```  
   **Response**:
   ```json
   {
       "success": "True"
   }
   ```

2. **Calling a Method With Positional Arguments**  
   Example: Calling `get_salenote` on `sale.order` with `partner_id` as `3`.  
   URL:  
   ```
   GET http://localhost:8069/api/sale.order/method/get_salenote/?token=1ec448c54a004165b4c0da976b227260&args=[3]
   ```  
   **Response**:
   ```json
   {
       "success": "sale note"
   }
   ```

3. **Calling a Method With Keyword Arguments**  
   Example: Calling `magento_update_warehouse` with {
        "order_id": "Magento order ID",
        "items": [
            {
              "order_line_id": "Magento order line ID",
              "warehouse_source_code": "Source codes in Magento",
              "tracking_number": "Tracking Number"
             }
        ]
    }.  
   URL:  
   ```
   GET http://localhost:8069/api/sale.order/method/magento_update_warehouse/?token=1ec448c54a004165b4c0da976b227260&kwargs={
        "order_id": "Magento order ID",
        "items": [
            {
              "order_line_id": "Magento order line ID",
              "warehouse_source_code": "Source codes in Magento",
              "tracking_number": "Tracking Number"
             }
        ]
    }
   ```  
   **Response**:
   ```json
   {
       "success": "12"
   }
   ```
    
   ```
   GET http://localhost:8069/api/sale.order/method/magento_update_tracking_number/?token=1ec448c54a004165b4c0da976b227260&kwargs={
        "order_id": "Magento order ID",
        "items": [
            {
              "order_line_id": "Magento order line ID",
              "warehouse_source_code": "Source codes in Magento",
              "tracking_number": "Tracking Number"
             }
        ]
    }
   ```  
   **Response**:
   ```json
   {
       "success": "12"
   }
   ```

---

#### **Response**:
- **On Success (HTTP 200)**:  
  Returns the result of the method call.  
  Example:
  ```json
  {
      "success": "Method result"
  }
  ```

- **On Failure (HTTP 404)**:  
  If the user token is invalid:  
  ```json
  {
      "error": "Invalid User Token"
  }
  ```

- **On Failure (HTTP 400 or 500)**:  
  If the model is not found or an exception occurs during the method call:  
  ```json
  {
      "error": "Model Not Found or <error_message>"
  }
  ```

---

#### **Notes**:
1. **Security**: Ensure the user has proper access rights to call methods on the specified record.
2. **Arguments**: 
   - Positional arguments must be passed in JSON format in the `args` query parameter.
   - Keyword arguments must be passed in JSON format in the `kwargs` query parameter.
3. **Error Handling**: 
   - If the `model` does not exist or the `method_name` is invalid, a detailed error message will be returned.
   - Invalid tokens or missing tokens will result in an "Invalid User Token" error.
   