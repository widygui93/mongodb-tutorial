* Secara sederhana, Transactions adalah menggabungkan beberapa operasi database dalam satu transaction, dimana transactions akan dianggap berhasil jika semua operasi sukses dan transactions akan dianggap gagal jika salah satu operasi gagal
* Jika transactions gagal , maka seluruh operasi yang sukses sebelumnya harus dibatalkan (rollback)
* Fitur transactions dalam MongoDB hanya bisa jalan di cluster (replica set), tidak di single node
* Di dalam cluster, MongoDB akan memiliki primary data dan secondary data

#### MongoDB Cluster Replica Set

![[Pasted image 20230226103427.png]]

* 1 cluster ada 3 mongoDB
* Saat menyimpan data di Mongo1 maka data akan di duplicate ke Mongo2 dan Mongo3
* Hal ini untuk mendistribusikan proses operasi Read dan/atau write ke MongoDB-nya
* Jadi saat high traffic maka load nya bisa di distribusikan ke node mongoDB yang lain
* Di dalam satu node MongoDB tidak dianjurkan memiliki data primary lebih dari satu. Contoh di Mongo1 hanya terdapat satu product (primary) dan data product (secondary) ada di Mongo2 dan Mongo3
* Hal ini agar jika Mongo1 down maka data product masih pertinggal di Mongo2 dan Mongo3
* Hanya bisa operasi write (insert, update, delete) di data primary
* Untuk operasi read (select) bisa di data secondary atau primary

| Function | Keterangan |
| --- | ------------ |
| session.startTransaction() | memulai transaction
| session.commitTransaction() | commit transaction |
| session.abortTransaction() | Membatalkan transaction |

#### Read Preferences
Read Preferences adalah bagaimana MongoDB mengkontrol dari mana membaca data.
* primary : semua query diambil dari primary replica set
* primaryPreferences: semua query diambil dari primary replica set, namun jika tidak ada primary replica set (karena down atau mati) maka di ambil dari secondary replica set
* secondary: semua query diambil dari secondary replica set
* secondaryPreferences: semua query diambil dari secondary replica set, namun jika tidak ada secondary replica set, maka di ambil dari primary replica set
* nearest: semua query diambil dari replica set (primary atau secondary) yang paling murah network latency nya

#### Read Concern
Read Concern adalah bagaimana MongoDB mengkontrol data yang kita dapatkan.
* local: Data akan didapatkan di local node
* available: Data akan didapatkan dimanapun (tidak pedulu node mana)
* majority: Data akan didapatkan di mayoritas data di semua node. Jika ada 3 node maka akan dapat dari 2 node agar data yang diambil beneran konsisten. (Jumlah node / 2) + 1. data di ambil dari 2 node dan di compare untuk di ambil data yang paling baru
* linearizable: Data akan dipastikan data yang paling baru di semua node
* snapshot: Data akan di ambil dari mayoritas snapshot (data yang telah di commit) di semua node

#### Write Concern
Write Concern adalah bagaimana MongoDB mengkontrol operasi write (insert, update, delete)
* {number} : operasi dianggap sukses jika sudah berhasil melakukan operasi write di node sejumlah {number}
* majority: operasi dianggap sukses jika sudah berhasil melakukan operasi write di mayoritas node

E.g // Setting replication
```
rs.initiate(
	{
		_id : 'my-mongo-set',
		members: [
			{ _id : 0, host : "mongo1:27017" },
			{ _id : 1, host : "mongo2:27017" },
			{ _id : 2, host : "mongo3:27017" }
		]
	}
);
```
// Create collection
```
db.createCollection("products");
db.createCollection("orders");
```
// Insert products
```
db.products.insertMany([
	{
		_id: 1,
		name: "Indomie ayam bawang",
		price: new NumberLong(2000),
		quantity: 10
	},
	{
		_id: 2,
		name: "Mie Sedap",
		price: new NumberLong(2000),
		quantity: 10
	}
]);
```
// Sample commit transaction
```
var session = db.getMongo().startSession( { readPreference: { mode: "primary" } } );

session.startTransaction( { readConcern: { level: "majority" }, writeConcern: { w: "majority" } } );

session.getDatabase("test").orders.insertOne({
	_id: new ObjectId(),
	total: new NumberLong(8000),
	items: [
		{
			product_id: 1,
			price: new NumberLong(2000),
			quantity: new NumberInt(2)
		},
		{
			product_id: 2,
			price: new NumberLong(2000),
			quantity: new NumberInt(2)
		}
	]
});

session.getDatabase("test").products.updateOne({
	_id: 1
}, {
	$inc: {
		quantity: -2
	}
});

session.getDatabase("test").products.updateOne({
	_id: 2
}, {
	$inc: {
		quantity: -2
	}
});

session.commitTransaction();

session.endSession();

```