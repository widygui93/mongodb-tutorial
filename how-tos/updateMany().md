#### Syntax updateMany() Function
```
db.collection.updateMany(
	{}, // filter
	{}, // update
	{}, // option
);
```
#### Example updateMany() Function
// update products set tags = ["food"] where category = "food" and tags is null
```
db.products.updateMany(
	{
		$and: [
			{ category:{ $eq: "food"} },
			{ tags: { $exists: false} }
		]
	},
	{
		$set: { tags: ["food"] }
	}
);
```

// update products set wrong = "wrong"
```
db.products.updateMany(
	{},
	{
		$set: { wrong: "wrong" }
	}
);
```

update with `$unset`
```
db.products.updateMany(
	{},
	[
		{ $unset: ["wrong"] }
	]
);
```