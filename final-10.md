
# Final Test 10

Check below all the statements that are true about the way MongoDB handled this query.

## Answer

* The query returned 120,477 documents.

No, "nReturned" is 83057.

* The query used an index to figure out which documents match the find criteria.

No, "FETCH" is used to match documents.
 
* The query scanned every document in the collection.

Yes, all documents are scanned (totalDocsExamined) 

* The query avoided sorting the documents because it was able to use an index's ordering.

Yes, there is not "SORT" stage.
