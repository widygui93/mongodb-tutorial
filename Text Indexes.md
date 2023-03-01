#### Syntax Text Index
```
db.collection.createIndex({
	field1: "text",
	field2: "text"
}, {
	weights: {
		field1: 10,
		field2: 5
	}
});
```
E.g.  // create index text
```
db.products.createIndex({
	name: "text",
	category: "text",
	tags: "text"
}, {
	weights: {
		name: 10,
		category: 5,
		tags: 1
	}
});
```
// search products with text "mie"
```
db.products.find({
	$text: {
		$search: "mie"
	}
});
```
// search products with text "mie" OR "laptop"
```
db.products.find({
	$text: {
		$search: "mie laptop"
	}
});
```
// search products with text "mie sedap"
```
db.products.find({
	$text: {
		$search: '"mie sedap"'
	}
})
```
// search products with text "mie" and NOT "sedap"
```
db.products.find({
	$text: {
		$search: "mei -sedap"
	}
})
```