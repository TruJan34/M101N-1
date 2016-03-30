# Homework 2.3


## Answer

Define Post model, specify id, initialize collections and created date:
```
public class Post
{
    [BsonId]
    public ObjectId Id { get; set; }

    public string Author { get; set; }

    public string Title { get; set; }

    public string Content { get; set; }

    public IEnumerable<string> Tags { get; set; } = new List<string>();

    public DateTime CreatedAtUtc { get; set; } = DateTime.UtcNow;

    public IEnumerable<Comment> Comments { get; set; } = new List<Comment>();
}
```

Define Comment model:
```
public class Comment
{
    public string Author { get; set; }

    public string Content { get; set; }

    public DateTime CreatedAtUtc { get; set; } = DateTime.UtcNow;
}
```

Define query to display latest posts:
```
var recentPosts = await blogContext.Posts
                            .Find(post => true)
                            .SortByDescending(post => post.CreatedAtUtc)
                            .Limit(10)
                            .ToListAsync();
``` 

Define query to submit post:
```
var post = new Post
{
    Title = model.Title,
    Content = model.Content,
    Tags = model.Tags.Split(new[] { "," }, StringSplitOptions.RemoveEmptyEntries),
    Author = User.Identity.Name,
};

await blogContext.Posts.InsertOneAsync(post);
```

Define query to view Post
```
var post = await blogContext.Posts.Find(Builders<Post>.Filter.Eq("_id", ObjectId.Parse(id))).FirstOrDefaultAsync();
```

Define query to display posts by tag:
```
var posts = await blogContext.Posts
                        .Find(Builders<Post>.Filter.All(post => post.Tags, new[] { tag }))
                        .ToListAsync();
```

Define query to post new comment:
```
await blogContext.Posts.UpdateOneAsync(
    Builders<Post>.Filter.Eq("_id", ObjectId.Parse(model.PostId)),
    Builders<Post>.Update.Push(post => post.Comments, comment));
```