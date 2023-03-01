#### Syntax replaceOne() Function
```
db.collection.replaceOne(
	{}, // filter
	{}, // replacement
	{}, // option
);
```

#### Example replaceOne() Function
// replace document with id 14
```
db.products.replaceOne(
	{ _id: 14 },
	{
		name: "Adidas Pulseboost HD running shoes sepatu lari pria",
		price: new NumberLong(1100000),
		category: "shoes",
		tags: ["adidas","shoes","running"]
	}
);
```
