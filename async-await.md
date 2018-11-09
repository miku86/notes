# Async Await

- write async code that reads like sync code
- inside a function marked as `async`, you can place `await` in front of a promise
- the execution of the `async` function gets paused until the promise is resolved

Promise:

```js
function fetchUrl(id) {
  return fetch(`https://.../${id}`)
    .then((response) => response.json())
    .then((data) => data.name);
}
const result = fetchUrl(123);
console.log(result); // => miku86
```

Async Await:

```js
async function fetchUrl(id) {
  const response = await fetch(`https://.../${id}`);
  const data = await response.json();
  return data.name;
}
const result = fetchUrl(123);
console.log(result); // => miku86
```
