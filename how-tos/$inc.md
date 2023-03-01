#### Syntax $inc Operator
```
db.collection.update(
	{}, // query
	{
		$inc: {
			field: 1, // increment
			field: -1 // decrement
		}
	}
)
```
#### Example $inc Operator
// update products set stock = stock + 10
```
db.products.updateMany(
	{},
	{
		$inc: {
			stock: 10
		}
	}
)
```