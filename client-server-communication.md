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

* CRUD: Create => `POST`, Read => `GET`, Update => `PUT`, Delete => `DELETE`
* minimum request: what: `GET /index.html HTTP/1.1` and where: `Host: www.example.com`
* minimum response: `HTTP/1.1 200 OK` and `Content-Length: 16824` and the requested document
* AJAX(old: XHR => new: Fetch) to reload data when needed with JavaScript

---

## HTTP/1

Example of Usage:

```
nc google.com 80
GET / HTTP/1.1
```

* additional Methods to CRUD: `HEAD` and `OPTIONS`
* common Response Headers: `Content-Length`, `Content-Type`, `Last-Modified`, `Cache-Control`
* REST work very well with HTTP: `REpresentational State Transfer`
* Network Architecture, different Layers: Ethernet => IP (talk to other machines) => TCP(have multiple streams of data between these machines) => HTTP
* Problem: Head of Line Blocking
* Every time TCP Handshake for a connection => `Connection: keep-alive`
* _Bundler for JavaScript and Images is very important for Performance_

---

## HTTPS

* uses TLS for Encryption
* uses Authentication (againts Man in the Middle Attack)
* _always use HTTPS_
* TLS uses Chain of Trust (e.g. through Certificate by Let's Encrypt)
* TLS uses Encryption and Hashing
* Encryption through Public-Private-Key Method
* Hashing through SHA256 or SHA512
* Certificate Authority Signatures: Hash of Document gets encrypted

* TLS Handshake Step by Step:
  1. Server sends you a Certificate including a Public Key, Domain and a CAS
  1. Client checks if Domain and CAS are correct and valid
  1. Client generates random key for this connection and encrypts it with the Servers Public Key
* check: badssl.com

---

## HTTP/2

* Problems of HTTP/1:

  * Head of Line Blocking: one request is blocking all other requests.
    We can handle 6 connections in parallel.
    With 100 requests, we need 17 requests per connection.
    A roundtrip of request and response needs ~30ms, so the overall loading time is 0,5s.
  * Uncompressed Header: 100kb per 100 requests
  * Security

* Improvements from HTTP/2 to HTTP/1:
  * Multiplexing for HOL: only one connection with a Stream and Frames
  * Header Compressing with HPACK
* Optimizations for HTTP/1 that are now anti-patterns in HTTP/2:
  * No Concatenation and Spriting needed, because it makes Caching inefficient
  * Minifying is very good
  * Use CDN (https)

---

## Security

* common security problems like CORS, CSRF, XSS
* same origin policy
* always validate user input server-side!
