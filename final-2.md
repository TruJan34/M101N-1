# Final Test 2

This problem is a little tricky because a recipient may appear more than once in the To list for a message. You will need to fix that in a stage of the aggregation before doing your grouping and counting of (sender, recipient) pairs

## Answer

* unwind recipients
* remove duplicates by $addToSet
* unwind and group by From, To to calculate amount

You could receive following error:
```
"Exceeded memory limit for $group, but didn't allow external sort. Pass allowDiskUse:true to opt in.",
```

So, do not forget to allow disk use.

```
db.messages.aggregate([
	{
	    $unwind:"$headers.To"
	}, 
	{
	$group: 
	    {
	        _id: { id: $_id, "From": "$headers.From" ,"To": "$headers.To"}, 
	        to :{ $addToSet: "$headers.To"}
        }
	}, 
	{
	    $unwind: "$to"
	},
	{
	$group: 
        {
	        _id: { "From": "$_id.From", "To": "$_id.To" }, 
	        "amount": { $sum: 1}
	    }
	}, 
	{
		$sort:{"amount": -1}
	},
	{
		$limit : 1
 	}
 ], {allowDiskUse:true})
```