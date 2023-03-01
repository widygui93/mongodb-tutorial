| Function | Keterangan |
| --- | ---------- |
| db.collection.insertMany() | Insert document secara banyak sekaligus |
| db.collection.updateMany() | Update document secara banyak sekaligus |
| db.collection.deleteMany() | Delete document secara banyak sekaligus |
| db.collection.bulkWrite() | Melakukan operasi write (insert, update, delete) secara banyak sekaligus |

#### Supported Bulk Write Operation
* insertOne
* updateOne
* updateMany
* replaceOne
* deleteOne
* deleteMany

#### Syntax bulkWrite() Function
```
db.collection.bulkWrite([
	{
		// operation 1
	},
	{
		// operation 2
	},
	{
		// operation n
	}
])
```

#### Example bulkWrite() Function
```
db.customers.bulkWrite([
	{
		insertOne: {
			_id: "eko",
			full_name: "eko"
		}
	},
	{
		insertOne: {
			_id: "kurniawan",
			full_name: "kurniawan"
		}
	},
	{
		updateMany: {
			filter: {
				_id: {
					$in: ["eko", "kurniawan"]
				}
			},
			update: {
				$set: {
					full_name: "eko kurniawan"
				}
			}
		}
	}
]);
```