# MongoDB Cheat Sheet

## Show All Databases

```javascript
show dbs
```

<details>
<summary>Result</summary>

```javascript
admin   0.000GB
config  0.000GB
local   0.000GB
phone   0.000GB
test    0.000GB
```

</details>

## Show Current Database

```javascript
db;
```

<details>
<summary>Result</summary>

```javascript
test;
```

</details>

## Create Or Switch Database

```javascript
use acme
```

<details>
<summary>Result</summary>

```javascript
switched to db acme
```

</details>

## Drop

```javascript
db.dropDatabase();
```

<details>
<summary>Result</summary>

```javascript
{ "ok" : 1 }
```

</details>

## Create Collection

```javascript
db.createCollection("posts");
```

<details>
<summary>Result</summary>

```javascript
{ "ok" : 1 }
```

</details>

## Show Collections

```javascript
show collections
```

<details>
<summary>Result</summary>

```javascript
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

```javascript
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
<summary>Result</summary>

```javascript
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
<summary>Result</summary>

```javascript
{ "_id" : ObjectId("61f181ff079ff92d683f39cb"), "title" : "Post One", "body" : "Body of post one", "category" : "News", "tags" : [ "news", "events" ], "user" : { "name" : "John Doe", "status" : "author" }, "date" : "Wed Jan 26 2022 18:16:47 GMT+0100 (CET)" }
{ "_id" : ObjectId("61f1820e079ff92d683f39cc"), "title" : "Post Two", "body" : "Body of post two", "category" : "Technology", "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)" }
{ "_id" : ObjectId("61f1820e079ff92d683f39cd"), "title" : "Post Three", "body" : "Body of post three", "category" : "News", "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)" }
{ "_id" : ObjectId("61f1820e079ff92d683f39ce"), "title" : "Post Four", "body" : "Body of post three", "category" : "Entertainment", "date" : "Wed Jan 26 2022 18:17:02 GMT+0100 (CET)" }
```

</details>

## Get All Rows Formatted

```javascript
db.posts.find().pretty();
```

<details>
<summary>Result</summary>

```javascript
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
<summary>Result</summary>

```javascript

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
<summary>Result</summary>

```javascript

```

</details>

## Count Rows

```javascript
db.posts.find().count();
db.posts.find({ category: "news" }).count();
```

<details>
<summary>Result</summary>

```javascript

```

</details>

## Limit Rows

```javascript
db.posts.find().limit(2).pretty();
```

<details>
<summary>Result</summary>

```javascript

```

</details>

## Chaining

```javascript
db.posts.find().limit(2).sort({ title: 1 }).pretty();
```

<details>
<summary>Result</summary>

```javascript

```

</details>

## Foreach

```javascript
db.posts.find().forEach(function (doc) {
  print("Blog Post: " + doc.title);
});
```

<details>
<summary>Result</summary>

```javascript

```

</details>

## Find One Row

```javascript
db.posts.findOne({ category: "News" });
```

<details>
<summary>Result</summary>

```javascript

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
<summary>Result</summary>

```javascript

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
```

<details>
<summary>Result</summary>

```javascript

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

```javascript

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

```javascript

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

```javascript

```

</details>

## Delete Row

```javascript
db.posts.remove({ title: "Post Four" });
```

<details>
<summary>Result</summary>

```javascript

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

```javascript

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
<summary>Result</summary>

```javascript

```

</details>

## Add Index

```javascript
db.posts.createIndex({ title: "text" });
```

<details>
<summary>Result</summary>

```javascript

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
<summary>Result</summary>

```javascript

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

```javascript

```

</details>
