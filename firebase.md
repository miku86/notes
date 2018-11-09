# Firebase

## Basics

- Firebase = Company
- Firebase Firestore = Realtime, noSQL, Cloud Database

## Setup

- add new Firestore at https://console.firebase.google.com/
- use code snippets for auth and paste it to `firebase.js`

- get/read/query data:

```js
db.collection(collectionName)
  .where(key, comparison, value) // additional selector ("city", "===", "Stuttgart")
  .orderBy(key, order) // additional order ("name", "desc")
  .limit(number) // additional limit (3)
  .get(); // getting a snapshot, iterate and .data()
```

- realtime updating data:

```js
db.collection(collectionName)
  .onSnapshot((snap) => {
    let changes = snap.docChanges();
    changes.forEach((change) => {}});
  });
```

- add data:

```js
db.collection(collectionName).add(obj);
```

- delete data:

```js
db.collection(collectionName)
  .doc(id)
  .delete();
```

- update data:

```js
db.collection(collectionName)
  .doc(id)
  .update({ key: value });
```
