# Final Test 6

Now suppose that basic inserts into the collection, which only include the last name, first name and student_id, are too slow (we can't do enough of them per second from our program). What could potentially improve the speed of inserts. Check all that apply.

## Answer

* Add an index on last_name, first_name if one does not already exist.

No, Adding index will add additional overhead for inserts.

* Remove all indexes from the collection, leaving only the index on _id in place

Yes, Removing indexes will improve performance.

* Provide a hint to MongoDB that it should not use an index for the inserts

No, it is not possible to do that, because after insert index should be rebuilt.

* Set w=0, j=0 on writes

Yes, it will improve performance.

* Build a replica set and insert data into the secondary nodes to free up the primary nodes.

No, it's not possible to write to secondary, only read.