| Function | Keterangan |
| --- | ---------- |
| db.collection.deleteOne(query) | Menghapus satu document pertama yang sesuai dengan kondisi query |
| db.collection.deleteMany(query) | Menghapus banyak document yang sesuai dengan kondisi query |

#### Example deleteOne() Function
```
db.customers.deleteOne({
	_id: "spammer"
});
```
#### Example deleteMany() Function
```
db.customers.deleteMany({
	_id: {
		$regex: "spammer"
	}
});
```