#### Syntax $meta Operator
```
db.collection.find({
	$text: {
		$search: "query"
	}
}, {
	score: {
		$meta: "textScore"
	}
})
```

#### example $meta operator
// select *, score from products where $search like "monitor"
```
db.products.find({
	$text: {
		$search: "monitor"
	}
},{
	score: {
		$meta: "textScore"
	}
})
```