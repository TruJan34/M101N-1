# Homework 5.4

In this problem you will calculate the number of people who live in a zip code in the US where the city starts with a digit. We will take that to mean they don't really live in a city.

## Answer

Steps are:
* Project city first char (but we basically could use regex)
* Match first char to number
* Group all records and calculate sum

```
db.zips.aggregate([
    {
        $project:
        {
            pop:1,
            first_char: { $substr : ["$city",0,1] }
        }
    },
    {
        $match:
        {
            "first_char": { $in: [ /^[0-9]/] }
        }
    },
    {
        $group: { "_id":null, "sum": {"$sum":"$pop"} }
    }
])
```