# Homework 4.2

Suppose you have a collection called tweets whose documents contain information about the created_at time of the tweet and the user's followers_count at the time they issued the tweet. What can you infer from the following explain output?

## Answer

No query return 10 documents ("nReturned" : 10)
```
The query returns 251120 documents.
```

Yes ("totalDocsExamined" : 251120)
```
The query examines 251120 documents.
```

No ("totalDocsExamined" : 251120)
```
The query is a covered query.
```

Yes, IXSCAN is used ("created_at_-1")
```
The query uses an index to determine the order in which to return result documents.
```

No, IXSCAN is not used, but rather FETCH
```
The query uses an index to determine which documents match.
```
