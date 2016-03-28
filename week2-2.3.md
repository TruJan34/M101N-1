# Homework 2.3

Download the handout from the Download Handout link above, and unpack it.

This is the beginning of the blog project with the UI for creating and logging in blog authors, but nothing to display posts.

The project uses ASP.NET MVC5. You should open the solution file (.sln) in Visual Studio and recognize a typical project. We have used the included template and haven't pulled in any extra dependencies.

The project won't compile immediately as there are missing pieces you'll need to fill out. These pieces are marked with XXX in a comment. You shouldn't need to touch any other code. First, in User.cs, you'll need to add in the contents of the User object. Second, in AccountController, you'll need to insert a user and retrieve a user by email.

The blog stores its data in the "blog" database in the "users" collection. Here are two example documents from the users collection. You can insert these if you'd like, but you don't need to.

```
> db.users.find()
{ "_id" : ObjectId("54c272a9122ea91adc328696"), "Name" : "Craig", "Email" : "craig@craig.com" }
{ "_id" : ObjectId("54c27f50122ea914546658be"), "Name" : "Andrew", "Email" : "andrews@andrew.com" }
```
Once you have the project working, the following steps should work.

Click "Register" on the home page and register a user.
Click "Login" on login with the user you just created.
Ok, now it's time to validate that you got it all working.

## Answer

It is quite straightforward:
* Define User POCO
* Define find User query
* Define create User operation

```
public class User
{
    [BsonId]
    public ObjectId Id { get; set; }

    public string Name { get; set; }

    public string Email { get; set; }
}

var user = await blogContext.Users.Find(userEntity => userEntity.Email == model.Email).FirstOrDefaultAsync();

await blogContext.Users.InsertOneAsync(new User
{
    Name = model.Name,
    Email = model.Email
});
```

And do not register camel case convention :)
```
ConventionRegistry.Register("CamelCaseConvention", new ConventionPack { new CamelCaseElementNameConvention() }, type => true);
```
