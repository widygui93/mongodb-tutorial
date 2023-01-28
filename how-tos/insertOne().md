Syntax:

```
db.<name-of-collection>.insertOne(document)
```

e.g:

```
db.customers.insertOne({
	name: "widy"
});
```

or

```
db.orders.insertOne({
	_id: new ObjectId(),
	total: new NumberLong("8000"),
	items: [
		{
			product_id: 1,
			price: new NumberLong("2000"),
			quantity: new NumberInt(2)
		},
		{
			product_id: 2,
			price: new NumberLong("2000"),
			quantity: new NumberInt(2)
		}
	]
});
```