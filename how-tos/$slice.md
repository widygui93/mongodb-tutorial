#### Syntax $slice Operator
```
db.collection.find({
	// query
},{
	field: {
		$slice: 2 // slice size
	}
})
```

#### example $slice operator
// select _id, name, price, category, tags[0,2] from products
```
db.products.find({}, {
    tags: {
        $slice: 2
    }
});
```

// select _id, name, price, category, tags[last 2] from products
```
db.products.find({}, {
    tags: {
        $slice: -2
    }
});
```

// select _id, name, price, category, tags[from, limit] from products
```
db.products.find({}, {
    tags: {
        $slice: [1, 1]
    }
});
```