# Intro to Backend

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

* Goals: How do web sites handle user input? Build HTML forms and the validation and escaping logic needed to handle user input correctly.

* `form` for form
* `input` for input field
* `label` for label field
* `select` for dropdown
* `input name="q"` for input field that adds `?q=` to the address
* `input type="submit"` same as pressing Enter
* `input type="password"` stars instead of clear text, but clear text in url
* `input type="checkbox"` for checkbox
* `input type="radio"` for radiobutton, need all the same name
* `input value="one"` parameter `q=one` gets sent
* `form action="https://google.com/search"` sends query to uri
* URL Encoding happens
* `form method="post"`
* GET includes parameters in URL <=> POST includes parameters in the request body
* GET can be cached <=> POST don't get cached
* GET shouldn't change the server <=> POST may change the server
* GET used for fetching documents <=> POST used for updating data on the server
* GET Requests with Links <=> POST Request with Forms
* always validate for user input and man in the middle input

---

## Templates

* Goals: How do web sites produce neatly formatted output for users to see?

---

## Databases

* Goals: How do web sites store data? Use both SQL databases and the Google App Engine datastore in this program.

---

## User Accounts & Security

* Goals: What's a cookie and what does it have to do with logging in a user? How do web sites use cookies, passwords, and other components to provide security?
