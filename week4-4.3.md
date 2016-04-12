# Homework 4.3

Your assignment is to make the following pages fast:

The blog home page (http://localhost:57912/)
The posts page where it displays posts by tag (http://localhost:57912/Home/Posts?tag=Van)
The tag should be whatever tag we wish to use.

By fast, we mean that an index should satisfy these queries such that we only need to scan the number of documents we are going to return.

## Answer

Main queries are:
* Find the most resent 10 posts
* Find the most resent 10 posts by tags

```
var recentPosts = await blogContext.Posts.Find(x => true)
                .SortByDescending(x => x.CreatedAtUtc)
                .Limit(10)
                .ToListAsync();
```

```             
if (tag != null)
{
    filter = x => x.Tags.Contains(tag);
}
                
var posts = await blogContext.Posts.Find(filter)
                .SortByDescending(x => x.CreatedAtUtc)
                .Limit(10)
                .ToListAsync();
```

These queries will require creation of following indexes:
```
db.posts.createIndex({ CreatedAtUtc: -1 })
db.posts.createIndex({ Tags: -1, CreatedAtUtc: -1 })
```