# Client Server Communication

Source: https://www.udacity.com/course/client-server-communication--ud897

## Table of Content

1. HTTP’s Request Response Cycle
2. HTTP/1
3. HTTPS
4. HTTP/2
5. Security

---

## HTTP’s Request Response Cycle

Goal:

* Learn about HTTP's request and response cycle.
* What makes up an HTTP requests and response?
* What originates an HTTP request and how do they relate to one another?

- CRUD: Create => `POST`, Read => `GET`, Update => `PUT`, Delete => `DELETE`
- minimum request: what: `GET /index.html HTTP/1.1` and where: `Host: www.example.com`
- minimum response: `HTTP/1.1 200 OK` and `Content-Length: 16824` and the requested document
- AJAX(old: XHR => new: Fetch) to reload data when needed with JavaScript







## HTTP/1

Goal:

* Find out how HTTP/1 is used in practice.
* Map the requests and response types from lesson 1 into HTTP verbs and response codes & headers.

## HTTPS

Goal:

* How does HTTPS differ from HTTP? TLS, cryptography, and Certificate Authorities.
* HTTP Mixed Content issues.

## HTTP/2

Goal:

* Learn how HTTP/2 improves on and extends HTTP/1.
* Look at optimizations for HTTP/1 that are now anti-patterns in HTTP/2.

## Security

Goal:

* Look at and resolve common security problems like CORS, CSRF, XSS, and more!
