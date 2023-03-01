#### Syntax $rename Operator
```
db.collection.update(
	{}, // query
	{
		$rename: {
			field1: "newFieldName1",
			field2: "newFieldName2"
		}
	}
)
```
#### Example $rename Operator
// alter table customers change name full_name
```
db.customers.updateMany(
	{},
	{
		$rename: {
			name: "full_name"
		}
	}
)
```