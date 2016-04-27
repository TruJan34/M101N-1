# Final Test 4

When you are done, the following functionality will be in place:

* When you are logged in, and you view a post in its own page (/Home/Post/<post_id>), each post will have a number of "Likes".
* When you click on the "Likes" button, it gets incremented by one.
* You can like a comment as many times as you wish; each click will increment it by one.
* You can even like your own comments. 

## Answer

We need the update query that increment particular comment by index:
```
var field = string.Format("Comments.{0}.Likes", model.Index);

Builders<Post>.Update.Inc(field, 1));
```

