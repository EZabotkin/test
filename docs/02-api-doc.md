# API Documentation

This document provides an overview of the **User and Partner API**, including endpoints, parameters, and response structures. It covers how to retrieve user and partner data and manage service plans.

## Endpoints Overview

### 1. **Get User Information**

**Endpoint**: `/api/external/user`  
**Method**: `GET`

#### Description:
Retrieves user details with optional filtering and pagination.

#### Parameters:
| Name        | In     | Description                                   | Type     | Example        |
|-------------|--------|-----------------------------------------------|----------|----------------|
| user_id     | query  | Unique user identifier (optional).            | string   | "3453255"     |
| from        | query  | Pagination start timestamp (optional).        | integer  | 1633046400000000000 |
| to          | query  | Pagination end timestamp (optional).          | integer  | 1633132800000000000 |
| limit       | query  | Limit of records to return (optional).        | integer  | 100            |
| provider_id | query  | Partner ID to which the user belongs (optional).| string  | "2323"        |

#### Response:
```json
{
  "user_id": "3453255",
  "provider_id": "2323",
  "status": "active",
  "type": "basic",
  "zone": "us"
}
```

---

### 2. **Get Partner Information**

**Endpoint**: `/api/partner`  
**Method**: `GET`

#### Description:
Retrieves partner details. `provider_id` is required.

#### Parameters:
| Name        | In     | Description                                   | Type     | Example  |
|-------------|--------|-----------------------------------------------|----------|----------|
| provider_id | query  | Unique partner identifier (required).         | string   | "2323"  |
| status      | query  | Partner operation state (optional).           | string   | "active"|

#### Response:
```json
{
  "provider_id": "2323",
  "status": "active"
}
```

---

### 3. **Get Service Plans**

**Endpoint**: `/api/plans`  
**Method**: `GET`

#### Description:
Retrieves a list of service plans available to a user based on their provider.

#### Parameters:
| Name        | In     | Description                                   | Type     | Example         |
|-------------|--------|-----------------------------------------------|----------|-----------------|
| user_type   | query  | Comma-separated user types to filter plans.   | string   | "basic,advanced" |
| provider_id | query  | Partner ID associated with the user.          | string   | "2323"         |

#### Response:
```json
{
  "plans": [
    {
      "plan_id": "plan123",
      "name": "Premium Plan",
      "user_types": ["basic", "advanced"]
    }
  ]
}
```

### 4. **Create a Service Plan**

**Endpoint**: `/api/plans`  
**Method**: `POST`

#### Description:
Creates a new service plan. Requires Basic authentication.

#### Request Body:
```json
{
  "name": "New Plan",
  "user_types": ["basic", "company"],
  "provider_id": "2323"
}
```

#### Response:
```json
{
  "plan_id": "plan456",
  "name": "New Plan"
}
```

## Authentication

**Scheme**: Basic Authentication  
**Header**: `Authorization: Basic <encoded_credentials>`

## Notes
- All timestamps are in nanoseconds.
- User role transitions and subscription management rely on provider-specific configurations.
- API supports pagination and filtering for improved flexibility.

For further details, refer to the [OpenAPI specification](api-doc.yaml) or contact the API team.

