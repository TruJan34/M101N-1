# Homework 2.3

Download the students.json file from the Download Handout link and import it into your local Mongo instance with this command:

```
mongoimport -d school -c students < students.json
```
This dataset holds the same type of data as last week's grade collection, but it's modeled differently. You might want to start by inspecting it in the Mongo shell.

Write a program in the language of your choice that will remove the lowest homework score for each student. Since there is a single document for each student containing an array of scores, you will need to update the scores array and remove the homework.

Remember, just remove a homework score. Don't remove a quiz or an exam!

To verify that you have completed this task correctly, provide the identity (in the form of their _id) of the student with the highest average in the class with following query that uses the aggregation framework. The answer will appear in the _id field of the resulting document.

```
db.students.aggregate( { '$unwind' : '$scores' } , { '$group' : { '_id' : '$_id' , 'average' : { $avg : '$scores.score' } } } , { '$sort' : { 'average' : -1 } } , { '$limit' : 1 } )
```

## Answer

In console to find homeworks:
* unwind scores array
* match only homeworks
* find homework with min score

To remove scores:
* match right array element with min score (additionally "scores.type":"homework" could be added)
* unset found element
 
```
db.students
    .aggregate(
        { $unwind : "$scores" },
        { $match: { "scores.type": "homework" } },
        { $group : { _id: "$_id" , minscore : { $min : "$scores.score" } } }
    )
    .forEach(function(doc) {
        db.students.update({ _id: doc._id, "scores.score": doc.minscore }, { $unset: { "scores.$": "" } } )
    })
```

Or using C# language:

```
var badHomeworks = studentsCollection.Aggregate()
    .Unwind("scores")
    .Match(Builders<BsonDocument>.Filter.Eq("scores.type", "homework"))
    .Group(new BsonDocument { { "_id", "$_id" }, { "minscore", new BsonDocument("$min", "$scores.score") } })
    .ToList();

foreach (var homework in badHomeworks)
{
    var builder = Builders<BsonDocument>.Filter;
    var filter = builder.Eq("_id", homework["_id"]) & builder.Eq("scores.score", homework["minscore"]);

    var unset = Builders<BsonDocument>.Update.Unset("scores.$");

    studentsCollection.UpdateOne(filter, unset);
}
```