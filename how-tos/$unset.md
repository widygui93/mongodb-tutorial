#### Syntax $unset Operator
```
db.collection.update(
	{}, // query
	{
		$unset: {
			field1: "",
			field2: ""
		}
	}
)
```