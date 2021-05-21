# MongoDB Cheat Sheet

## Show All Databases

```sh
show dbs
```

## Show Current Database

```sh
db
```

## Create Or Switch Database

```sh
use acme
```

## Drop

```sh
db.dropDatabase()
```

## Create Collection

```sh
db.createCollection('posts')
```

## Show Collections

```sh
show collections
```

## Insert Row

```sh
db.posts.insert({
  title: 'Post One',
  body: 'Body of post one',
  category: 'News',
  tags: ['news', 'events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})
```

## Insert Multiple Rows

```sh
db.posts.insertMany([
  {
    title: 'Post Two',
    body: 'Body of post two',
    category: 'Technology',
    date: Date()
  },
  {
    title: 'Post Three',
    body: 'Body of post three',
    category: 'News',
    date: Date()
  },
  {
    title: 'Post Four',
    body: 'Body of post three',
    category: 'Entertainment',
    date: Date()
  }
])
```

## Get All Rows

```sh
db.posts.find()
```

## Get All Rows Formatted

```sh
db.posts.find().pretty()
```

## Find Rows

```sh
db.posts.find({ category: 'News' })
```

## Sort Rows

```sh
# asc
db.posts.find().sort({ title: 1 }).pretty()
# desc
db.posts.find().sort({ title: -1 }).pretty()
```

## Count Rows

```sh
db.posts.find().count()
db.posts.find({ category: 'news' }).count()
```

## Limit Rows

```sh
db.posts.find().limit(2).pretty()
```

## Chaining

```sh
db.posts.find().limit(2).sort({ title: 1 }).pretty()
```

## Foreach

```sh
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})
```

## Find One Row

```sh
db.posts.findOne({ category: 'News' })
```

## Find Specific Fields

```sh
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})
```

## Update Row

```sh
db.posts.update({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})
```

## Update Specific Field

```sh
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})
```

## Increment Field (\$inc)

```sh
db.posts.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})
```

## Rename Field

```sh
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})
```

## Delete Row

```sh
db.posts.remove({ title: 'Post Four' })
```

## Sub-Documents

```sh
db.posts.update({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'Mary Williams',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Harry White',
        date: Date()
      }
    ]
  }
})
```

## Find By Element in Array (\$elemMatch)

```sh
db.posts.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)
```

## Add Index

```sh
db.posts.createIndex({ title: 'text' })
```

## Text Search

```sh
db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
})
```

## Greater & Less Than

```sh
db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })
```
