# B) API Reference Entry

## Create a New Task

### HTTP Method and Endpoint

**Method:** `POST`
**Endpoint:** `/api/tasks`

### Description

This endpoint allows an authenticated user to create a new task in a project management application.

### Request Parameters

| Parameter     | Data Type | Required/Optional | Description                                                          |
| ------------- | --------- | ----------------- | -------------------------------------------------------------------- |
| `title`       | String    | Required          | The name or title of the task.                                       |
| `description` | String    | Optional          | Additional information about the task.                               |
| `assignee_id` | Integer   | Required          | The user ID of the person assigned to the task.                      |
| `due_date`    | String    | Required          | The date when the task must be completed, using `YYYY-MM-DD` format. |
| `priority`    | String    | Required          | The priority level of the task. Must be `low`, `medium`, or `high`.  |

### Required Request Headers

| Header          | Required | Description                                                     |
| --------------- | -------- | --------------------------------------------------------------- |
| `Authorization` | Yes      | Contains the Bearer access token used to authenticate the user. |
| `Content-Type`  | Yes      | Must be `application/json` because the request body is JSON.    |

Example:

```text
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

### Example Request Body

```json
{
  "title": "Complete Python assignment",
  "description": "Finish the Exercise B API documentation",
  "assignee_id": 25,
  "due_date": "2026-10-15",
  "priority": "high"
}
```

### HTTP Response Codes

| Status Code                 | Explanation                                                          |
| --------------------------- | -------------------------------------------------------------------- |
| `201 Created`               | The task was successfully created.                                   |
| `400 Bad Request`           | The request contains invalid or missing information.                 |
| `401 Unauthorized`          | The authentication token is missing, invalid, or expired.            |
| `403 Forbidden`             | The authenticated user does not have permission to create a task.    |
| `404 Not Found`             | The specified assignee or related project could not be found.        |
| `409 Conflict`              | The request conflicts with existing data, such as a duplicate task.  |
| `422 Unprocessable Entity`  | The request format is valid, but one or more values fail validation. |
| `500 Internal Server Error` | An unexpected problem occurred on the server.                        |

### Example Successful Response

```json
{
  "id": 101,
  "title": "Complete Python assignment",
  "description": "Finish the Exercise B API documentation",
  "assignee_id": 25,
  "due_date": "2026-10-15",
  "priority": "high",
  "status": "created",
  "created_at": "2026-10-08T14:30:00Z"
}
```

The `201 Created` response indicates that the new task was successfully created and assigned a unique task ID.
