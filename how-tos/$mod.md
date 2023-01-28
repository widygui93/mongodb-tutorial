#### Syntax $mod operator
```
db.collection.find({
	field: {
		$mod: [ division, remainder]
	}
})
```

example $mod operator
// select * from products where price % 5 = 0
```
db.products.find({
	price: {
		$mod: [5, 0]
	}
});
```