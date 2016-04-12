# Homework 4.1

Suppose you have a collection with the following indexes:

```
> db.products.getIndexes()
[
    ...
	{
		"v" : 1,
		"key" : {
			"price" : -1
		},
		"ns" : "store.products",
		"name" : "price_-1"
	},
	{
		"v" : 1,
		"key" : {
			"category" : 1,
			"brand" : 1
		},
		"ns" : "store.products",
		"name" : "category_1_brand_1"
	}
    ...
```

Which of the following queries can utilize at least one index to find all matching documents or to sort? Check all that apply.

## Answer

Will use price index:
```
db.products.find( { $and : [ { price : { $gt : 30 } },{ price : { $lt : 50 } } ] } ).sort( { brand : 1 } )
```

Will not use index because ```{ category : 1, brand : 1 }``` index can only support ```sort({category : 1, brand : 1})``` or ```sort({category : -1, brand : -1})``` sorting:  
```
db.products.find( { brand : 'GE' } ).sort( { category : 1, brand : -1 } )
```

Will use price index:
```
db.products.find( { 'brand' : "GE" } ).sort( { price : 1 } )
```

Following query won't use ```{ category : 1, brand : 1 }``` index because 'category' is missing in query: 
```
db.products.find( { 'brand' : "GE" } )