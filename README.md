## API Overview

This API delivers complete, up-to-date information on movies, TV shows, and actors, including trailers, awards, biographies, filmographies, and other valuable details. It’s ideal for powering apps, websites, and platforms that need reliable entertainment data.

## Version
V1

## Available Endpoints
### Title
path: /titles
returns title acording to filters / sorting query parameters provided

### Title Rating
path: /titles/ratings
returns title rating and votes number

### Seasons and Episodes
path: / /titles/series/{id}
returns array of episodes only with episode id, episode number and season number in ascending order

### Seasons Number
path: /titles/seasons/{id}
returns number of seasons for the series

### Episode
path: /titles/episode/{id}
returns episode according to filters / sorting query parameters provided

## Request and Response Format

All API requests and responses use JSON unless otherwise stated. Requests should include the following HTTP header:

- Content-Type: application/json

If authentication is required, also include:

- Authorization: Bearer <your_api_token>

1. Request Structure
A typical API request consists of:

Component	 - Description
HTTP Method	 - The action to perform (e.g., GET, POST, PUT, DELETE).
Endpoint	 - The URL path to the resource (e.g., /movies/{id}).
Headers	     - Key-value pairs providing metadata (e.g., Content-Type, Authorization).
Path Params	 - Variables embedded in the URL path (e.g., {id}).
Query Params - 	Optional parameters appended to the URL (e.g., ?limit=10&page=2).
Body	     - JSON object containing data for POST/PUT requests.

Example – POST Request:


POST /movies HTTP/1.1
Host: api.example.com
Authorization: Bearer your_api_token
Content-Type: application/json

Request Body:


{
  "title": "Example Movie",
  "year": 2023,
  "genres": ["Drama", "Thriller"],
  "runtime_minutes": 115
}

2. Response Structure
A typical API response contains:

Field	Type	Description
data	object/array	The main payload containing requested or newly created resources.
meta	object	Metadata about the response (pagination info, totals, etc.).
error	boolean	Indicates if an error occurred (true or false).
message	string	Human-readable description of the result or error.
code	integer	HTTP status code or custom application code.

Example – Success (200 OK):

{
  "data": {
    "id": "tt1234567",
    "title": "Example Movie",
    "year": 2023,
    "genres": ["Drama", "Thriller"],
    "runtime_minutes": 115,
    "trailer_url": "https://youtube.com/watch?v=example",
    "awards": {
      "nominations": 3,
      "wins": 1
    },
    "cast": [
      { "name": "John Doe", "role": "Lead Actor" },
      { "name": "Jane Smith", "role": "Supporting Actress" }
    ]
  },
  "meta": {
    "request_id": "abc123",
    "timestamp": "2025-08-10T17:45:00Z"
  },
  "error": false,
  "message": "Movie details retrieved successfully",
  "code": 200
}
Example – Error (404 Not Found):

json
Copy
Edit
{
  "data": null,
  "meta": {
    "request_id": "xyz789",
    "timestamp": "2025-08-10T17:45:00Z"
  },
  "error": true,
  "message": "Movie not found",
  "code": 404
}
