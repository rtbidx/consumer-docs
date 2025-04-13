# RTBX CB
This is a callback consumer for real-time bidder program

# API Documentation

## Overview
This document provides instructions on how to use the `/report` and `/api-key` endpoints of the application. These endpoints are designed for external parties to generate reports and obtain API keys for authentication.

### Base URL
All API endpoints described in this documentation are accessible at:
```
https://impbid.com
```

---

## 1. `/api-key` Endpoint

### Description
The `/api-key` endpoint is used to generate an API key for authentication. The API key is required to access the `/report` endpoint.

### Method
`POST`

### Request Headers
- `Content-Type: application/json`

### Request Body
```json
{
  "UserName": "<your-username>",
  "Password": "<your-password>"
}
```

### Response
- On success:
  ```json
  {
    "api_key": "<generated-api-key>"
  }
  ```
- On failure: An appropriate error message with an HTTP status code.

---

## 2. `/report` Endpoint

### Description
The `/report` endpoint is used to fetch report data for a specific date range and exchange. Authentication is required via the `X-API-Key` header.

### Method
`GET`

### Request Headers
- `X-API-Key: <your-api-key>`

### Query Parameters
- `start_date`: The start date of the report in `YYYY-MM-DD` format (required).
- `end_date`: The end date of the report in `YYYY-MM-DD` format (required).
- `type`: The type of report (optional, currently only non-JSON formats are supported).

### Response
- On success: A JSON object containing the report data.
- On failure: An appropriate error message with an HTTP status code.

### Example Request
```
GET /report?start_date=2025-04-01&end_date=2025-04-10&type=summary HTTP/1.1
Host: <your-host>
X-API-Key: <your-api-key>
```

### Example Response
```json
[
  {
    "date": "2025-04-01",
    "data": "..."
  },
  {
    "date": "2025-04-02",
    "data": "..."
  }
]
```

---

## Notes
- Ensure that the `X-API-Key` is kept secure and not shared with unauthorized parties.
- Dates must be in the `YYYY-MM-DD` format; otherwise, the request will fail.
- For any issues, contact the support team.
