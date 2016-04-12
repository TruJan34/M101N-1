# Homework 4.2

In this problem you will analyze a profile log taken from a mongoDB instance. To start, please download sysprofile.json from Download Handout link and import it with the following command:

```
mongoimport -d m101 -c profile < sysprofile.json
```

Now query the profile data, looking for all queries to the students collection in the database school2, sorted in order of decreasing latency. What is the latency of the longest running operation to the collection, in milliseconds?

## Answer

Basically, we need to filter by namespace and sort by running time. 
```
db.profile.find({"ns":"school2.students"}, {_id:0, "millis": 1}).sort({"millis": -1}).limit(1)
```