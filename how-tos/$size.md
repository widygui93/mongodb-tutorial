#### Syntax $size operator
```
db.collection.find({
	fields: {
		$size: 1 // length
	}
})
```

#### Example $size operator
// select * from products where size(tags) = 3
```
db.products.find({
    tags: {
        $size: 3
    }
});
```

Note: `$size` does not accept ranges of values.
