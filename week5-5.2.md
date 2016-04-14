# Homework 5.2

Please calculate the average population of cities in California (abbreviation CA) and New York (NY) (taken together) with populations over 25,000. 

## Answer

Steps are:
* Filter by state (NY and CA)
* group by state and city
* sum population for city
* filter cities with population less than 2500
* group all record with averate population

```
db.zips.aggregate([
    {
        $match:
        {
            $or:[{"state":"NY"},{state:"CA"}]
        }
    },
    {
        $group:
        {
            _id:{state:"$state", city:"$city"}, "pop":{"$sum":"$pop"}
        }
    },
    {
        $match: {"pop": { $gt:25000 } }
    },
    {
        $group: { _id:null, avg: { $avg:"$pop" } }
    }
])
```