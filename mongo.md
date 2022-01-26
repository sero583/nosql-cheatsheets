# MongoDB Cheat Sheet

## Show All Databases

```javascript
show dbs
```

<details>
<summary>Result</summary>

```json
admin   0.000GB
config  0.000GB
local   0.000GB
test    0.000GB
```

</details>

## Show Current Database

```javascript
db;
```

<details>
<summary>Result</summary>

```json
test;
```

</details>

## Create Or Switch Database

```javascript
use acme
```

<details>
<summary>Result</summary>

```json
switched to db acme
```

</details>

## Drop

```javascript
db.dropDatabase();
```

<details>
<summary>Ackchyuall Result</summary>

```json
{ "ok": 1 }
```

</details>

## Create Collection

```javascript
db.createCollection("posts");
```

<details>
<summary>Ackchyuall Result</summary>

```json
{ "ok": 1 }
```

</details>

## Show Collections

```javascript
show collections
```

<details>
<summary>Result</summary>

```json
posts;
```

</details>

## Insert Row

```javascript
db.posts.insert({
  title: "Post One",
  body: "Body of post one",
  category: "News",
  tags: ["news", "events"],
  user: {
    name: "John Doe",
    status: "author",
  },
  date: Date(),
});
```

<details>
<summary>Result</summary>

```json
WriteResult({ nInserted: 1 });
```

</details>

## Insert Multiple Rows

```javascript
db.posts.insertMany([
  {
    title: "Post Two",
    body: "Body of post two",
    category: "Technology",
    date: Date(),
  },
  {
    title: "Post Three",
    body: "Body of post three",
    category: "News",
    date: Date(),
  },
  {
    title: "Post Four",
    body: "Body of post three",
    category: "Entertainment",
    date: Date(),
  },
]);
```

<details>
<summary>Ackchyuall Result</summary>

```json
{
    "acknowledged" : true,
    "insertedIds" : [
    ObjectId("61f1820e079ff92d683f39cc"),
    ObjectId("61f1820e079ff92d683f39cd"),
    ObjectId("61f1820e079ff92d683f39ce")
    ]
}
```

</details>

## Get All Rows

```javascript
db.posts.find();
```

<details>
<summary>Ackchyuall Result</summary>

```json
{
    "_id" : ObjectId("61f185ba079ff92d683f39cf"),
    "title" : "Post One",
    "body" : "Body of post one",
    "category" : "News",
    "tags" : [
        "news",
        "events"
    ],
    "user" : {
        "name" : "John Doe",
        "status" : "author"
    },
    "date" : "Wed Jan 26 2022 18:32:42 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f185c0079ff92d683f39d0"),
    "title" : "Post Two",
    "body" : "Body of post two",
    "category" : "Technology",
    "date" : "Wed Jan 26 2022 18:32:48 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f185c0079ff92d683f39d1"),
    "title" : "Post Three",
    "body" : "Body of post three",
    "category" : "News",
    "date" : "Wed Jan 26 2022 18:32:48 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f185c0079ff92d683f39d2"),
    "title" : "Post Four",
    "body" : "Body of post three",
    "category" : "Entertainment",
    "date" : "Wed Jan 26 2022 18:32:48 GMT+0100 (CET)"
}
```

</details>

## Get All Rows Formatted

```javascript
db.posts.find().pretty();
```

<details>
<summary>Ackchyuall Result</summary>

```json
{
    "_id" : ObjectId("61f181ff079ff92d683f39cb"),
    "title" : "Post One",
    "body" : "Body of post one",
    "category" : "News",
    "tags" : [
    "news",
    "events"
    ],
    "user" : {
    "name" : "John Doe",
    "status" : "author"
    },
    "date" : "Wed Jan 26 2022 18:16:47 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f1820e079ff92d683f39cc"),
    "title" : "Post Two",
    "body" : "Body of post two",
    "category" : "Technology",
    "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f1820e079ff92d683f39cd"),
    "title" : "Post Three",
    "body" : "Body of post three",
    "category" : "News",
    "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f1820e079ff92d683f39ce"),
    "title" : "Post Four",
    "body" : "Body of post three",
    "category" : "Entertainment",
    "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)"
}
```

</details>

## Find Rows

```javascript
db.posts.find({ category: "News" });
```

<details>
<summary>Ackchyuall Result</summary>

```json
{
    "_id" : ObjectId("61f185ba079ff92d683f39cf"),
    "title" : "Post One",
    "body" : "Body of post one",
    "category" : "News",
    "tags" : [
        "news",
        "events"
    ],
    "user" : {
        "name" : "John Doe",
        "status" : "author"
    },
    "date" : "Wed Jan 26 2022 18:32:42 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f185c0079ff92d683f39d1"),
    "title" : "Post Three",
    "body" : "Body of post three",
    "category" : "News",
    "date" : "Wed Jan 26 2022 18:32:48 GMT+0100 (CET)"
}
```

</details>

## Sort Rows

```javascript
# asc
db.posts.find().sort({ title: 1 }).pretty()
# desc
db.posts.find().sort({ title: -1 }).pretty()
```

<details>
<summary>Result 1</summary>

```json
{
    "_id" : ObjectId("61f1820e079ff92d683f39ce"),
    "title" : "Post Four",
    "body" : "Body of post three",
    "category" : "Entertainment",
    "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f181ff079ff92d683f39cb"),
    "title" : "Post One",
    "body" : "Body of post one",
    "category" : "News",
    "tags" : [
    "news",
    "events"
    ],
    "user" : {
    "name" : "John Doe",
    "status" : "author"
    },
    "date" : "Wed Jan 26 2022 18:16:47 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f1820e079ff92d683f39cd"),
    "title" : "Post Three",
    "body" : "Body of post three",
    "category" : "News",
    "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f1820e079ff92d683f39cc"),
    "title" : "Post Two",
    "body" : "Body of post two",
    "category" : "Technology",
    "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)"
}
```

</details>

<details>
<summary>Result -1</summary>

```json
{
    "_id" : ObjectId("61f1820e079ff92d683f39cc"),
    "title" : "Post Two",
    "body" : "Body of post two",
    "category" : "Technology",
    "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f1820e079ff92d683f39cd"),
    "title" : "Post Three",
    "body" : "Body of post three",
    "category" : "News",
    "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f181ff079ff92d683f39cb"),
    "title" : "Post One",
    "body" : "Body of post one",
    "category" : "News",
    "tags" : [
    "news",
    "events"
    ],
    "user" : {
    "name" : "John Doe",
    "status" : "author"
    },
    "date" : "Wed Jan 26 2022 18:16:47 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f1820e079ff92d683f39ce"),
    "title" : "Post Four",
    "body" : "Body of post three",
    "category" : "Entertainment",
    "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)"
}
```

</details>

## Count Rows

```javascript
db.posts.find().count();
db.posts.find({ category: "news" }).count(); // kleines n
```

<details>
<summary>Result</summary>

```json
4;
0;
```

</details>

## Limit Rows

```javascript
db.posts.find().limit(2).pretty();
```

<details>
<summary>Ackchyuall Result</summary>

```json
{
    "_id" : ObjectId("61f181ff079ff92d683f39cb"),
    "title" : "Post One",
    "body" : "Body of post one",
    "category" : "News",
    "tags" : [
    "news",
    "events"
    ],
    "user" : {
    "name" : "John Doe",
    "status" : "author"
    },
    "date" : "Wed Jan 26 2022 18:16:47 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f1820e079ff92d683f39cc"),
    "title" : "Post Two",
    "body" : "Body of post two",
    "category" : "Technology",
    "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)"
}
```

</details>

## Chaining

```javascript
db.posts.find().limit(2).sort({ title: 1 }).pretty();
```

<details>
<summary>Ackchyuall Result</summary>

```json
{
    "_id" : ObjectId("61f1820e079ff92d683f39ce"),
    "title" : "Post Four",
    "body" : "Body of post three",
    "category" : "Entertainment",
    "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)"
}
{
    "_id" : ObjectId("61f181ff079ff92d683f39cb"),
    "title" : "Post One",
    "body" : "Body of post one",
    "category" : "News",
    "tags" : [
    "news",
    "events"
    ],
    "user" : {
    "name" : "John Doe",
    "status" : "author"
    },
    "date" : "Wed Jan 26 2022 18:16:47 GMT+0100 (CET)"
}
```

</details>

## Foreach

```javascript
db.posts.find().forEach(function (doc) {
  print("Blog Post: " + doc.title);
});
db.posts.find().forEach((doc) => print(`Blog Post: ${doc.title}`));
```

<details>
<summary>Result</summary>

```json
Blog Post: Post One
Blog Post: Post Two
Blog Post: Post Three
Blog Post: Post Four
```

</details>

## Find One Row

```javascript
db.posts.findOne({ category: "News" });
```

<details>
<summary>Ackchyuall Result</summary>

```json
{
    "_id" : ObjectId("61f181ff079ff92d683f39cb"),
    "title" : "Post One",
    "body" : "Body of post one",
    "category" : "News",
    "tags" : [
    "news",
    "events"
    ],
    "user" : {
    "name" : "John Doe",
    "status" : "author"
    },
    "date" : "Wed Jan 26 2022 18:16:47 GMT+0100 (CET)"
}
```

</details>

## Find Specific Fields

```javascript
db.posts.find(
  { title: "Post One" },
  {
    title: 1,
    author: 1,
  }
);
```

<details>
<summary>Ackchyuall Result</summary>

```json
{ "_id" : ObjectId("61f181ff079ff92d683f39cb"), "title" : "Post One" }
// hint: author gets ignored due to its {"user" : { "name" : "John Doe", "status" : "author" }}
```

</details>

## Update Row

```javascript
db.posts.update(
  { title: "Post Two" },
  {
    title: "Post Two",
    body: "New body for post 2",
    date: Date(),
  },
  {
    upsert: true,
  }
);
// {upsert: true} = no insert on unknown documents
```

<details>
<summary>Result</summary>

```json
WriteResult({ nMatched: 1, nUpserted: 0, nModified: 1 });
```

</details>

## Update Specific Field

```javascript
db.posts.update(
  { title: "Post Two" },
  {
    $set: {
      body: "Body for post 2",
      category: "Technology",
    },
  }
);
```

<details>
<summary>Result</summary>

```json
WriteResult({ nMatched: 1, nUpserted: 0, nModified: 1 });
```

</details>

## Increment Field (\$inc)

```javascript
db.posts.update(
  { title: "Post Two" },
  {
    $inc: {
      likes: 5,
    },
  }
);
```

<details>
<summary>Result</summary>

```json
WriteResult({ nMatched: 1, nUpserted: 0, nModified: 1 });
```

</details>

## Rename Field

```javascript
db.posts.update(
  { title: "Post Two" },
  {
    $rename: {
      likes: "views",
    },
  }
);
```

<details>
<summary>Result</summary>

```json
WriteResult({ nMatched: 1, nUpserted: 0, nModified: 1 });
```

</details>

## Delete Row

```javascript
db.posts.remove({ title: "Post Four" });
```

<details>
<summary>Result</summary>

```json
WriteResult({ nRemoved: 1 });
```

</details>

## Sub-Documents

```javascript
db.posts.update(
  { title: "Post One" },
  {
    $set: {
      comments: [
        {
          body: "Comment One",
          user: "Mary Williams",
          date: Date(),
        },
        {
          body: "Comment Two",
          user: "Harry White",
          date: Date(),
        },
      ],
    },
  }
);
```

<details>
<summary>Result</summary>

```json
WriteResult({ nMatched: 1, nUpserted: 0, nModified: 1 });
```

</details>

## Find By Element in Array (\$elemMatch)

```javascript
db.posts.find({
  comments: {
    $elemMatch: {
      user: "Mary Williams",
    },
  },
});
```

<details>
<summary>Ackchyuall Result</summary>

```json
{
    "_id" : ObjectId("61f185ba079ff92d683f39cf"),
    "title" : "Post One",
    "body" : "Body of post one",
    "category" : "News",
    "tags" : [
        "news",
        "events"
    ],
    "user" : {
        "name" : "John Doe",
        "status" : "author"
    },
    "date" : "Wed Jan 26 2022 18:32:42 GMT+0100 (CET)",
    "comments" : [
        {
            "body" : "Comment One",
            "user" : "Mary Williams",
            "date" : "Wed Jan 26 2022 18:34:44 GMT+0100 (CET)"
        },
        {
            "body" : "Comment Two",
            "user" : "Harry White",
            "date" : "Wed Jan 26 2022 18:34:44 GMT+0100 (CET)"
        }
    ]
}
```

</details>

## Add Index

```javascript
db.posts.createIndex({ title: "text" });
```

<details>
<summary>Ackchyuall Result</summary>

```json
{
  "numIndexesBefore": 1,
  "numIndexesAfter": 2,
  "createdCollectionAutomatically": false,
  "ok": 1
}
```

</details>

## Text Search

```javascript
db.posts.find({
  $text: {
    $search: '"Post O"',
  },
});
```

<details>
<summary>Ackchyuall Result</summary>

```json
{
    "_id" : ObjectId("61f185ba079ff92d683f39cf"),
    "title" : "Post One",
    "body" : "Body of post one",
    "category" : "News",
    "tags" : [
        "news",
        "events"
    ],
    "user" : {
        "name" : "John Doe",
        "status" : "author"
    },
    "date" : "Wed Jan 26 2022 18:32:42 GMT+0100 (CET)",
    "comments" : [
        {
            "body" : "Comment One",
            "user" : "Mary Williams",
            "date" : "Wed Jan 26 2022 18:34:44 GMT+0100 (CET)"
        },
        {
            "body" : "Comment Two",
            "user" : "Harry White",
            "date" : "Wed Jan 26 2022 18:34:44 GMT+0100 (CET)"
        }
    ]
}
```

</details>

## Greater & Less Than

```javascript
db.posts.find({ views: { $gt: 2 } });
db.posts.find({ views: { $gte: 7 } });
db.posts.find({ views: { $lt: 7 } });
db.posts.find({ views: { $lte: 7 } });
```

<details>
<summary>Result</summary>

```json


{
    "_id" : ObjectId("61f185c0079ff92d683f39d0"),
    "title" : "Post Two",
    "body" : "Body for post 2",
    "date" : "Wed Jan 26 2022 18:34:15 GMT+0100 (CET)",
    "category" : "Technology",
    "views" : 5
}
{
    "_id" : ObjectId("61f185c0079ff92d683f39d0"),
    "title" : "Post Two",
    "body" : "Body for post 2",
    "date" : "Wed Jan 26 2022 18:34:15 GMT+0100 (CET)",
    "category" : "Technology",
    "views" : 5
}
```

</details>

## Thanks to

[Brad Traversy](https://gist.github.com/bradtraversy/f407d642bdc3b31681bc7e56d95485b6) for giving the template!
