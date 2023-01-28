| Operator | Description |
| ---- | ---- |
| $exists | Mencocokkan document yang memiliki field tersebut (value: true/false) |
| $type | Mencocokkan document yang memiliki type field tersebut (value: string,int,bool,etc)|

Syntax:

```
db.collection.find({
	field: {
		$operator: value
	}
})
```

e.g:

// select * from products where category is null
```
db.products.find({
	category: {
		$exists: false
	}
})
```

// select * from products where type(category) = "string"
```
db.products.find({
	category: {
		$type: "string"
	}
})
```

// select * from products where type(price) in ("int", "long")
```
db.products.find({
	price: {
		$type: ["int", "long"]
	}
})
```
