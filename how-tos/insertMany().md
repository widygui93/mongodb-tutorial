Syntax:

```
db.<name-of-collection>.insertMany(array<document>)
```

e.g:

```
db.products.insertMany([
	{
		_id: 1,
		name: "indomie",
		price: new NumberInt(2000)
	},
	{
		_id: 2,
		name: "mie sedap",
		price: new NumberInt(2000)
	}
]);
```

or

```
db.products.insertMany([
	{
		_id: 1,
		name: "indomie",
		price: new NumberLong("2000")
	},
	{
		_id: 2,
		name: "mie sedap",
		price: new NumberLong("2000")
	}
]);
```