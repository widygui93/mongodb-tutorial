#### Syntax $text operator
```
db.collection.find({
	$text: {
		$search: "string",
		$language: "string", // optional
		$caseSensitive: "boolean", // optional
		$diacriticSensitive: "boolean" // optional
	}
});
```

Example $text operator
// create text index on products
```
db.products.createIndex({
    name: "text"
});
```

// select * from products where (name like "%mie%" or name like "%sedap%")
```
db.products.find({
	$text: {
		$search: "mie sedap"
	}
})
```

// select * from products where name like "%mie sedap%"
```
db.products.find({
	$text: {
		$search: '"mie sedap"'
	}
})
```

// select * from products where name like "%mie%" and name not like "%sedap%"
```
db.products.find({
	$text: {
		$search: "mie -sedap"
	}
})
```
note: A _negated_ term is a term that is prefixed by a minus sign `-`

// select * from products where name = "Tissue"
```
db.products.find({
	$text: {
		$search: "Tissue",
		$caseSensitive: true
	}
})
```