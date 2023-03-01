// use admin
note: mesti masuk ke database admin dulu

// Create user
```
db.createUser(
	{
		user: "mongo",
		pwd: "mongo",
		roles: ["userAdminAnyDatabase","readWriteAnyDatabase"]
	}
);
```