# Intro to Backennd

Source: https://www.udacity.com/course/intro-to-backend--ud171

## Table of Content

0. Primer
1. Forms and Inputs
1. Templates
1. Databases
1. User Accounts & Security

---

## Primer

* URI

  * `https://example.com:80/books?q=5&p=3#start`
  * protocol://host:port/path?query#fragment

* HTTP Request:

  * get `/books?q=5#start` of host
  * `GET /book?q=5 HTTP/1.1`
  * method /path version
  * query yes, fragment no

* HTTP Reponse:

  * `HTTP/1.1 200 OK`
  * version code phrase
  * `4xx` Client Error
  * `5xx` Server Error

## Forms and Inputs

* How do web sites handle user input?
* Build HTML forms and the validation and escaping logic needed to handle user input correctly.

---

## Templates

* How do web sites produce neatly formatted output for users to see?

---

## Databases

* How do web sites store data?
* Use both SQL databases and the Google App Engine datastore in this program.

---

## User Accounts & Security

* What's a cookie and what does it have to do with logging in a user?
* How do web sites use cookies, passwords, and other components to provide security?
