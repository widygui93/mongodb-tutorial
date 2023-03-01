* Menambahkan behaviour dan kemampuan tertentu terhadap index yang dibuat

#### TTL Index (Time to Live Index)
* TTL Index digunakan sebagai waktu hidup document di collection, artinya akan hilang dalam kurun waktu yang ditentukan secara otomotis.
* TTL Index hanya bisa digunakan di field dengan tipe data _Date_.
* Background mongodb akan secara regular menghapus data secara otomatis yang berjaan setiap 60 detik sekali

#### Syntax TTL Index
```
db.collections.createIndex({
	field: 1
}, {
	expireAfterSeconds: 10
});
```
E.g.  // Create TTL Index
```
db.sessions.createIndex({
	createdAt: 1
}, {
	expireAfterSeconds: 10
});
```
// Will expire after 10 seconds, but background job run every 60 seconds
```
db.sessions.insertOne({
	_id: 1,
	session: "session 1",
	createdAt: new Date()
});
```

#### Unique Index
* Memastikan bahwa field-field di index tersebut tidak menyimpan data duplicate.
* Misalnya, field _id merupakan unique index. Sehingga tidak bisa membuat document dengan field _id yang sama.

#### Syntax Unique Index
```
db.collections.createIndex({
	field: 1
}, {
	unique: true
});
```
E.g.  // Create unique index
```
db.customers.createIndex({
	email: 1
}, {
	unique: true
});
```
// failed duplicate email
```
db.customers.insertOne({
	_id: "gagal",
	full_name: "gagal",
	email: "riki@example.com"
});
```
![[Pasted image 20230225104419.png]]
