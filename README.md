# Daily Learning and Q&A

## 1. What is asynchronous programming in JavaScript/Node.js?

Asynchronous programming lets a program start work that may take time, such as a network request or file read, and continue with other work while waiting. When the operation completes, the program handles its result using callbacks, Promises, or `async`/`await`. Node.js uses an event loop to coordinate asynchronous operations without blocking the main thread.

```js
async function loadData() {
  const response = await fetch("/api/data");
  return response.json();
}
```

## 2. What is the Virtual DOM in React?

The Virtual DOM is a lightweight, in-memory representation of the user interface. When a component's state or props change, React compares the updated representation with the previous one and applies the necessary changes to the browser's DOM.

## 3. What is exception handling in Python?

Exception handling lets a program respond to errors that occur while it runs. A `try` block contains code that might fail, `except` handles an error, and `finally` runs whether or not an error occurred.

```python
try:
	number = int(input("Enter a number: "))
except ValueError:
	print("Please enter a valid integer.")
finally:
	print("Finished.")
```

## 4. What is a REST API, and how does it work?

A REST API allows software systems to communicate over HTTP by working with resources, such as users or orders. A client sends a request to an endpoint, and the server processes it and returns a response, often in JSON. Common HTTP methods are `GET` (read), `POST` (create), `PUT` or `PATCH` (update), and `DELETE` (remove). REST APIs are generally stateless: each request carries the information needed to process it.

## 5. What is cloud computing? Explain IaaS, PaaS, and SaaS.

Cloud computing provides computing resources over the internet, so organizations can use servers, platforms, or software without managing all the underlying infrastructure themselves.

- **IaaS (Infrastructure as a Service):** Provides virtual machines, storage, and networking. The customer manages the operating system and applications. Example: Amazon EC2.
- **PaaS (Platform as a Service):** Provides a managed platform for building and deploying applications, so developers can focus on application code. Example: Google App Engine.
- **SaaS (Software as a Service):** Provides a complete application over the internet. The provider manages the application and infrastructure. Example: Microsoft 365.
