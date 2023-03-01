* Authorization dilakukan untuk melakukan pengecekan apakah user memiliki hak akses untuk melakukan sebuah action
* Hak akses disimpan dalam bentuk role

#### Database Roles
Berikut database roles yang spesifik di satu database
| Role | Keterangan |
| --- | ---------- |
| read | Bisa membaca data di semua collection yang bukan sistem collection
| readWrite | Bisa membaca dan mengubah data di semua collection yang bukan sistem collection |
| dbAdmin | Bisa melakukan kemampuan administrasi database |
| userAdmin | Mampu membuat user dan role |
| dbOwner | Kombinasi readWrite, dbAdmin, dan userAdmin |

#### All Database Roles
Berikut database roles yang diapply di semua database
| Role | Keterangan |
| --- | --------- |
| readAnyDatabase | Seperti read role, tapi untuk semua database |
| readWriteAnyDatabase | Seperti readWrite role, tapi untuk semua database |
| dbAdminAnyDatabase | Seperti dbAdmin role, tapi untuk semua database |
| userAdminAnyDatabase | Seperti userAdmin role, tapi untuk semua database |

#### Backup & Restore Roles
| Role | Keterangan |
| --- | ---------- |
| backup | role untuk backup database |
| restore | role untuk restore database |

#### Superuser Roles
| Role | Keterangan |
| --- | -------- |
| root | bisa melakukan apapun |

#### Privileges
* Role diatas untuk level database dan merupakan role bawaan MongoDB
* untuk level collection perlu di buat privileges
* jika perlu role spesifik bisa di buatkan privileges

| Function | Keterangan |
| ----- | ---------- |
| db.createRole() | membuat role baru |
| db.getRoles() | mendapatkan semua roles |
| db.updateRole() | mengubah role |
| db.deleteRole() | menghapus role |

```
db.createRole({
	role: "name",
	privileges: [
		{
			resource: {
				db: "database",
				collection: "collection"
			},
			actions: ["action"]
		}
	],
	roles: [
		{
			role: "role",
			db: "database"
		}
	]
})
```
E.g. // create role
```
db.createRole({
	role: "find_and_insert",
	privileges: [],
	roles: [{role: "read", db: "test"}]
});
```
// Get all roles
```
db.getRoles({ showPrivileges: true });
```
// update role
```
db.updateRole("find_and_insert",{
	privileges: [
		{
			resource: {
				db: "test",
				collection: "products"
			},
			actions: [ "insert" ]
		}
	],
	roles: [{role: "read", db: "test"}]
});
```

// Add use with role
```
db.createUser({
	user: "widygui",
	pwd: "widy",
	roles: [ "find_and_insert" ]
});
```

// Insert product (SUCCESS)
```
db.products.insert({
	"_id" : 10,
	"name" : "iPad Pro 11 2020",
	"price" : NumberLong(20000000),
	"category" : "tablet",
	"tags" : [
		"apple",
		"ipad",
		"tablet",
	],
	"lastModifiedDate" : new Date(),
	"stock" : 10,
	"ratings" : [
		100
	]
});
```
// read product (SUCCESS)
```
db.products.find()
```
![[Pasted image 20230301214414.png]]

// Delete product (FAILED)
```
db.products.deleteOne({
	_id: 10
});
```
![[Pasted image 20230301214512.png]]

// Update product (FAILED)
```
db.products.updateOne({
	_id: 10
},{
	$set: {
		category: "food"
	}
});
```
![[Pasted image 20230301214611.png]]

// Insert Customer (FAILED)
```
db.customers.insertOne({
	_id: "kurniawan",
	name: "Eko Kurniawan Khannedy"
});
```
![[Pasted image 20230301214723.png]]