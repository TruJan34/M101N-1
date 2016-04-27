# Final Test 5

Now suppose you want to run the following query against the collection.

```
db.stuff.find({'a':{'$lt':10000}, 'b':{'$gt': 5000}}, {'a':1, 'c':1}).sort({'c':-1})
```

Which of the indexes could be used by MongoDB to assist in answering the query? Check all that apply.

## Answer

```
{'a':{'$lt':10000}, 'b':{'$gt': 5000}}
```
Could use: a_1_b_1

```
{'a':1, 'c':1}
```
Could use: a_1_c_1

```
{'c':-1}
```
Could use: c_1

Last two could also use: "a_1_b_1_c_-1"