* Tanpa Indexes, MongoDB akan melakukan collection scan saat query
* Index menyimpan spesifik field, lalu mengurutkan data field tersebut. Hal ini membantu dalam proses pencarian dalam bentuk range document (paging)
* Indexes bagus dalam melakukan operasi read (select) tapi kurang bagus dalam operasi write (create, update, delete). Karena saat write maka mongoDB akan melakukan operasi write di collection dan melakukan adjust ke indexes nya. Jadi 2 kali kerja.
* By default, field _id sudah dilakukan indexing
* Jika kita membutuhkan query terhadap lebih dari satu field, kita bisa membuat index untuk lebih dari satu field yaitu _compound indexes_
* Max _compound indexes_ adalah 32 fields
* Pakai explain() untuk cek apakah query kita melakukan index scan (IXSCAN) atau collection scan (COLLSCAN). Yang kita mau yaitu IXSCAN

| Function | Keterangan |
| --- | ------------ |
| db.collection.createIndex() | Membuat index di collection |
| db.collection.getIndexes() | Melihat semua index di collection |
| db.collection.dropIndex() | Menghapus index di collection |

#### Syntax Single Field Index
```
db.collection.createIndex({
	field: 1 // ascending
});
```
OR 
```
db.collection.createIndex({
	field: -1 // descending
})
```

#### Syntax Compound Field Index
```
db.collection.createIndex({
	field1: 1,
	field2: -1
})
```
E.g.  // Create index at category in products collection
```
db.products.createIndex({
	category: 1
});
```
// Get all indexes in products collection
```
db.products.getIndexes();
```
// Debugging query optimization
```
db.products.find({
	category: "food"
}).explain();
```
OR
```
db.products.find({}).sort({
	category: 1
}).explain();
```
Note: akan melakukan index scan karena filter maupun sorting menggunkan field "category" yang ada di dalam index

![[Pasted image 20230222213058.png]]

// Create index at price and tags in products collection
```
db.products.createIndex({
	stock: 1,
	tags: 1
});
```
// Debugging query optimization (will use IXSCAN)
```
db.products.find({
	stock: 10
}).explain();
```
OR
```
db.products.find({
	stock: 10,
	tags: "popular"
}).explain();
```
Note: karena saat create indexes mengunakan [stock, tags] maka saat query akan melakukan index scan karena masih dalam kombinasi indexes nya yaitu [stock] , [stock, tags]

![[Pasted image 20230222213826.png]]

// Debugging query optimization (will not use IXSCAN)
```
db.products.find({
	tags: "popular"
}).explain();
```
Note: tidak akan melakukan index scan karena bukan dalam kombinasi indexing yaitu [stock] , [stock, tags]
![[Pasted image 20230222213952.png]]
