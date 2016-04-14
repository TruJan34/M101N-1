# Homework 5.1

First, download the handout and unpack.

You can import the data with:

```
mongoimport -d blog -c posts --drop small_posts.json
```
Make sure that you're dropping the old collection if you already had data; it should now have 200 documents.

In this assignment you will use the aggregation framework to find the most frequent author of comments on your blog. We will be using the same basic dataset as last week, with posts and comments shortened considerably, and with many fewer documents.

## Answer

Few simple steps:
* Unwind comments array
* Group by author
* Sum number of record
* and sort descending 

```
db.posts.aggregate([
    {
        $unwind: "$comments"
    },
    {
        $group:
        {
            _id: { author: "$comments.author" },
            amount: { $sum:1 }
        }
    },
    {
        $sort: { "amount":-1 }
    },
    {
        $limit:1
    }
])
```