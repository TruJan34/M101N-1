# Homework 6.4

You have a sharded system with three shards and have sharded the collections "students" in the "school" database across those shards. The output of sh.status() when connected to mongos looks like this:

## Answer

* s1

```{ "student_id" : 2 } -->> { "student_id" : 3497 } on : s1 Timestamp(3, 2)``` 