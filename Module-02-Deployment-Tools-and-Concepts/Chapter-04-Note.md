# 🚀 FastAPI Development Guide

This section covers the core concepts of building robust APIs using FastAPI, focusing on request handling and data modeling.

---

## ⚡ FastAPI
**FastAPI** is a modern, high-performance web framework for building APIs with Python 3.8+ based on standard Python type hints.

* **Performance:** Built on Starlette and Pydantic, it is one of the fastest Python frameworks available, rivaling NodeJS and Go.
* **Auto-Documentation:** It automatically generates interactive API documentation via **Swagger UI** (at `/docs`) and **ReDoc** (at `/redoc`).
* **Type Safety:** By using Python type hints, FastAPI provides built-in data validation, serialization, and editor support (autocompletion).



---

## 📥 GET Request: Retrieving Data
In RESTful architecture, the **GET** method is used to retrieve a representation of a resource.

* **Read-Only:** GET requests are idempotent and should never modify server-side data.
* **Data Transfer:** Parameters are sent via the URL using:
    * **Path Parameters:** e.g., `/items/{item_id}`
    * **Query Parameters:** e.g., `/items?skip=0&limit=10`
* **Caching:** Browsers and servers can cache GET responses to optimize performance.
* **Security Note:** Sensitive data (passwords, tokens) should **never** be sent via GET, as URLs are visible in browser history and server logs.

---

## 📤 POST Request: Sending Data
The **POST** method is used to send data to the server to create or update a resource.

* **Request Body:** Data is included in the body of the HTTP request, typically in JSON format.
* **Non-Idempotent:** Unlike GET, multiple identical POST requests will usually result in multiple side effects (e.g., creating the same user twice).
* **Security:** More secure than GET for sensitive data because information is not exposed in the URL.
* **FastAPI Integration:** You define a Pydantic class to represent the "Body," and FastAPI handles the JSON-to-Object conversion automatically.



---

## 📋 FastAPI Response Model
The `response_model` is a parameter in the route decorator that defines the structure of the data sent back to the client.

* **Data Filtering:** This is its most critical feature. It allows you to return a database object while automatically filtering out sensitive fields (like `hashed_password`).
* **Validation:** It ensures the outgoing data matches your defined schema, preventing the API from accidentally sending malformed responses.
* **Serialization:** Automatically converts complex Python objects (like SQLAlchemy models) into standard JSON.
* **Implementation:** ```python
  @app.post("/users/", response_model=UserPublic)
  def create_user(user: UserCreate):
      return db_user