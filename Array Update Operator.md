| Operator | Keterangan|
| --- | -------- |
| $ | Mengubah data array pertama sesuai kondisi query |
| $[] | Mengubah semua data array sesuai kondisi query |
| $[identifier] | Mengubah semua data array yang sesuai kondisi arrayFilters |
| index | Mengubah data array sesuai dengan nomor index |
| $addToSet | Menambahkan value ke array, dihiraukan jika sudah ada |
| $pop | Menghapus element pertama (-1) atau terakhir (1) array |
| $pull | Menghapus semua element di array yang sesuai kondisi |
| $push | Menambahkan element ke array |
| $pullAll | Menghapus semua element di array |
| $each | Digunakan di $addToSet dan $push, untuk menambahkan multiple element |
| $position | Digunakan di $push untuk mengubah posisi saat menambahkan element |
| $slice | Digunakan di $push untuk menentukan jumlah maksimal element array |
| $sort | Digunakan untuk mengurutkan array setelah operasi $push |

#### Syntax $ Operator
```
db.collection.updateMany(
	{
		field: "value"
	},
	{
		$operator: {
			"field.$": "value"
		}
	}
)
```

E.g. //  update first element of array, query must include array fields
```
db.products.updateMany(
	{ ratings: 90 },
	{ 
		$set: {
			"field.$": 100
		}
	}
);
```

#### Syntax $[] Operator
```
db.collection.updateMany(
	{}, // query
	{
		$operator: {
			"field.$[]": "value"
		}
	}
)
```

E.g. //  update all element of array
```
db.products.updateMany(
	{},
	{
		$set: {
			"ratings.$[]": 100
		}
	}
)
```

#### Syntax $[identifier] Operator
```
db.collection.updateMany(
	{}, // query
	{
		$operator: {
			"field.$[element]": "value"
		}
	},
	{
		arrayFilters: [
			{
				element: { $operator: "value" }
			}
		]
	}

)
```

E.g.  // update element of array based on arrayFilters
```
db.products.updateMany(
	{},
	{
		$set: {
			"ratings.$[element]": 100
		}
	},
	{
		arrayFilters: [
			{
				element: { $gte: 80 }
			}
		]
	}
);
```

#### Syntax "index" Operator
```
db.collection.updateMany(
	{}, // query
	{
		$operator: {
			"field.<index>": "value"
		}
	}
)
```

E.g. // update element of array with given index
```
db.products.updateMany(
	{},
	{
		$set: {
			"ratings.0": 50,
			"ratings.1": 60
		}
	}
);
```

#### Syntax $addToSet Operator
```
db.collection.updateOne(
	{}, // query
	{
		$addToSet: {
			field: "value"
		}
	}
)
```

E.g.  // add "popular" to array if not exists
```
db.products.updateOne(
	{ _id: 1 },
	{
		$addToSet: {
			tags: "popular"
		}
	}
);
```

#### Syntax $pop Operator
```
db.collection.UpdateOne(
	{}, // query
	{
		$pop: {
			field: -1 // element pertama
		}
	}
)
```
E.g.  // remove first element of array
```
db.products.updateMany(
	{},
	{
		$pop: {
			ratings: -1
		}
	}
);
```
#### Syntax $pull Operator
```
db.collection.updateMany(
	{}, // query
	{
		$pull: {
			field: {
				$operator: "value"
			}
		}
	}
)
```
E.g.  // remove all element where ratings >= 80
```
db.products.updateMany(
	{}, // query
	{
		$pull: {
			ratings: {
				$gte: 80
			}
		}
	}
);
```
#### Syntax $push Operator
```
db.collection.UpdateMany(
	{}, // query
	{
		$push: {
			field: "value"
		}
	}
)
```
E.g.  // add 100 to ratings
```
db.products.updateMany(
	{},
	{
		$push: {
			ratings: 100
		}
	}
);
```
#### Syntax $pullAll Operator
```
db.collection.updateMany(
	{}, // query
	{
		$pullAll: {
			field: ["value"]
		}
	}
)
```
E.g. // remove element 100
```
db.products.updateMany(
	{},
	{
		$pullAll: {
			ratings: [100]
		}
	}
);
```
#### Syntax $each Operator
```
db.collection.updateMany(
	{}, // query
	{
		$operator: {
			field: {
				$each: ["value1","value2"]
			}
		}
	}
)
```
E.g.  // add 100, 200, 300 to ratings
```
db.products.updateMany(
	{},
	{
		$push: {
			ratings: {
				$each: [100,200,300]
			}
		}
	}
);
```
E.g. // add trending, popular to tags
```
db.products.updateMany(
	{},
	{
		$addToSet: {
			tags: {
				$each: ["trending","popular"]
			}
		}
	}
);
```
#### Syntax $position Operator
```
db.collection.UpdateMany(
	{}, // query
	{
		$push: {
			field: {
				each: ["value"],
				$position: 1 // index ke-1
			}
		}
	}
)
```
E.g.  // add hot in posititon 1
```
db.products.updateMany(
	{},
	{
		$push: {
			tags: {
				$each: ["hot"],
				$position: 1
			}
		}
	}
);
```
#### Syntax $slice Operator
```
db.collection.updateMany(
	{}, // query
	{
		$push: {
			field: {
				$each: ["value","value"],
				$slice: 1
			}
		}
	}
)
```
E.g. // add all element, but limit with slice
```
db.products.updateMany(
	{},
	{
		$push: {
			ratings: {
				$each: [100,200,300,400,500],
				$slice: -5 
				// -5 setelah di tambahkan akan ambil 5 data paling belakang
				// 5 setelah di tambahkan akan ambil 5 data paling depan
			}
		}
	}
)
```
#### Syntax $sort Operator
```
db.collection.UpdateMany(
	{}, // query
	{
		$push: {
			field: {
				$each: ["value"],
				$sort: 1 // asc
			}
		}
	}
)
```
E.g.  // add all element, and sort desc
```
db.products.updateMany(
	{},
	{
		$push: {
			ratings: {
				$each: [100,200,300,400,500],
				$sort: -1
			}
		}
	}
);
```