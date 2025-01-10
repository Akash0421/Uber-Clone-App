# Uber Clone App Backend API Documentation

## Authentication Endpoints

### Register New User
- **Method**: POST
- **Endpoint**: `/users/register`
- **Content-Type**: application/json

#### Description
Creates a new user account with the provided information and returns an authentication token.

#### Request Body Schema
```json
{
  "fullname": {
    "firstname": "string",    // required, min 3 characters
    "lastname": "string"      // optional, min 3 characters if provided
  },
  "email": "string",         // required, valid email format
  "password": "string"       // required, min 6 characters
}
```

#### Success Response
- **Status Code**: 201 Created
- **Response Body**:
```json
{
  "token": "JWT_TOKEN_STRING",
  "user": {
    "_id": "MONGODB_USER_ID",
    "fullname": {
      "firstname": "string",
      "lastname": "string"
    },
    "email": "string"
  }
}
```

#### Error Responses
- **Status Code**: 400 Bad Request
- **Condition**: Invalid input or validation errors
- **Response Body**:
```json
{
  "errors": [
    {
      "msg": "Error message",
      "param": "field_name",
      "location": "body"
    }
  ]
}
```

#### Example Usage
```bash
curl -X POST http://localhost:3000/users/register \
  -H "Content-Type: application/json" \
  -d '{
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com",
    "password": "password123"
  }'
```

#### Validation Rules
- First name: Minimum 3 characters
- Last name: Optional, but if provided, minimum 3 characters
- Email: Must be valid email format
- Password: Minimum 6 characters
