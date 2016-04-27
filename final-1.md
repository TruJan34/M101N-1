# Final Test 1

Construct a query to calculate the number of messages sent by Andrew Fastow, CFO, to Jeff Skilling, the president. Andrew Fastow's email addess was andrew.fastow@enron.com. Jeff Skilling's email was jeff.skilling@enron.com. 

## Answer

Steps are following:
* Unwind headers.To
* match From and To fields
* group by To (or null) and calculate number of records

```
 db.messages.aggregate([
    {
         $unwind: "$headers.To"
    },
    {
        $project: { "headers.From": 1, "headers.To": 1 }
    },
    {
        $match: { "headers.From": "andrew.fastow@enron.com", "headers.To": "jeff.skilling@enron.com"}
    },
    {
        $group: { "_id":"$headers.To", "sum": {"$sum":1}
    }
 }]);
```

