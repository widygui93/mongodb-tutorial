#### Syntax $currentDate Operator
```
db.collection.update(
	{}, // query
	{
		$currentDate: {
			field1: { $type: "date" },
			field2: { $type: "timestamp" }
		}
	}
)
```
#### Example $currentDate Operator
// update products set lastModifiedDate = current_date()
```
db.products.updateMany(
	{},
	{
		$currentDate: {
			lastModifiedDate: { $type: "date" }
		}
	}
)
```