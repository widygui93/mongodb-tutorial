* Digunakan untuk membuat index terhadap field yang belum diketahui atau field yang sering berubah-ubah

#### Syntax Wildcard Index
```
db.collection.createIndex({
	"field.$**": 1
})
```

E.g // membuat wilcard index
```
db.customers.createIndex({
	"customFields.$**": 1
});
```
// Insert many customers
```
db.customers.insertMany([
	{
		_id: "budi",
		full_name: "budi",
		customFields: {
			hobby: "gaming",
			university: "binus"
		}
	},
	{
		_id: "rosa",
		full_name: "rosa",
		customFields: {
			ipk: 3.2,
			university: "ugm"
		}
	},
	{
		_id: "riki",
		full_name: "riki",
		customFields: {
			passion: "gaming",
			university: "ui"
		}
	}
]);
```
// Debug wildcard index
```
db.customers.find({
	"customFields.hobby": "gaming"
}).explain();
```
