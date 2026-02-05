# REST API Client – Web Communication (C)

A command-line REST API client implemented in C, designed to interact with a remote
web service for user authentication and library management. The client supports
session handling via cookies, JWT-based authorization, and JSON request/response
processing.

Originally developed as part of a Communication Protocols assignment, this
project emphasizes low-level HTTP communication, request construction, and robust
client-side validation.

---

## Features

- User registration and authentication
- Session management using HTTP cookies
- JWT-based authorization for protected resources
- Access-controlled library operations
- Book retrieval, creation, and deletion
- Input validation and error handling
- JSON request construction and parsing
- Command-line interactive interface

---

## Supported Commands

The client interprets user commands entered via the console and executes the
corresponding HTTP requests.

### `register`
Registers a new user by sending a `POST` request with a username and password.
Credentials must be non-empty and must not contain spaces. Invalid input or duplicate
users result in server-side errors.

### `login`
Authenticates a user using a `POST` request. On success, the client stores the session
cookie returned by the server. Authentication fails if credentials are invalid or if
the user is already logged in.

### `enter_library`
Requests access to the library. If the user is authenticated, the server issues a JWT
token, which is stored by the client and used for subsequent authorized requests.
Unauthorized access results in HTTP `401`.

### `get_books`
Retrieves the list of all available books. Requires both authentication and a valid
library access token. Unauthorized or forbidden access results in HTTP `403`.

### `get_book`
Retrieves detailed information for a specific book identified by its ID. The client
validates the ID and ensures the user is authenticated and authorized before issuing
the request.

### `add_book`
Adds a new book to the library. Requires all book fields (`title`, `author`, `genre`,
`publisher`, `page_count`) to be provided and valid. The operation is permitted only
for authenticated users with library access.

### `delete_book`
Deletes a book identified by its ID. The client validates the ID and ensures proper
authorization before issuing the request.

### `logout`
Logs out the current user by clearing the stored session cookie and JWT token.

### `exit`
Terminates the client application.

---

## Implementation Details

- The client is built on top of a laboratory-provided HTTP skeleton, extended with
  support for `DELETE` requests and authorization tokens.
- HTTP `GET`, `POST`, and `DELETE` requests are constructed manually to ensure
  fine-grained control over headers and payloads.
- Client-side validation is performed before sending requests to prevent invalid input.
- Cookies and JWT tokens are extracted and stored locally for session persistence.

---

## Helper Functions

Several auxiliary functions were implemented to simplify client logic:
- `get_cookie` and `get_token` extract authentication data from server responses
- `compute_books` parses and formats book lists
- `read_book_info` reads and validates book data from user input

---

## JSON Parsing

Server responses are parsed using the **Parson** JSON library  
(https://github.com/kgabis/parson), chosen for its lightweight design, C-based
implementation, and ease of integration.

---

## How to Run

The project can be compiled and executed using:

```bash
make run
```
This command builds the client and runs the resulting executable.

## Conclusion

This project provided hands-on experience with low-level HTTP communication, REST API
interaction, authentication mechanisms, and robust input validation in C. It
strengthened my understanding of client-server architectures and secure web
communication at the protocol level.


