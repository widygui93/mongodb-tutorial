| Function | keterangan |
| --- | ---------------- |
| db.createUser() | Membuat user |
| db.getUsers() | Mendapatkan semua user |
| db.dropUser() | Menghapus user |
| db.updateUser() | Mengupdate user |
| db.changeUserPassword() | Mengubah user password |

// Create user with access read only
```
db.createUser(
	{
		user: "contoh",
		pwd: "contoh",
		roles: [{ role: "read", db: "test"}]
	}
);
```
// connect using
```
mongosh "mongodb://mongo:27017" --username contoh --authenticationDatabase test
```
jika berada di database selain database test (contoh database basic_mongo) maka akan error ketika di coba execute command
![[Pasted image 20230228145144.png]]

karena user contoh hanya ter-authentication di database test maka hanya bisa execute command di database test aja , tidak ada error yang terjadi
![[Pasted image 20230228145300.png]]

// get all users
```
db.getUsers()
```

// Change password for user contoh
```
db.changeUserPassword("contoh", "rahasia")
```
![[Pasted image 20230228150348.png]]
menggunakan password lama sudah tidak bisa login ke mongodb nya

// Drop user contoh
```
db.dropUser("contoh")
```
// before drop
![[Pasted image 20230228150618.png]]
// afer drop
![[Pasted image 20230228150647.png]]

// Update user
```
db.updateUser("contoh2",
	{
		roles: [
            { role: "read", db: "test" }
            ]
	}
)
```
before update user
![[Pasted image 20230228151434.png]]

after update user

![[Pasted image 20230228151525.png]]
