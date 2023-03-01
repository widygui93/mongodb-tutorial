#### Syntax $jsonSchema operator
```
db.collection.find({
	$jsonSchema: {
		// JSON Schema Object
	}
});
```

example $jsonSchema operator
// select * from products where name is not null and category is not null
```
db.products.find({
    $jsonSchema: {
        required: [ "name", "category"]
    }
});
```


// select * from products where name is not null and type(name) = 'string' and type(price) = 'long'
```
db.products.find({
    $jsonSchema: {
        required: [ "name"],
        properties: {
            name: {
                bsonType: "string"
            },
            price: {
                bsonType: "long"
            }
        }
    }
});
```

// select * from products where price <= 2500
```
db.products.find({
	$jsonSchema: {
		properties: {
			price: {
				maximum: 2500
			}
		}
	}
});
```

// select * from orders where count(items) <= 2
```
db.orders.find({
	$jsonSchema: {
		properties: {
			items: {
				maxItems: 2
			}
		}
	}
});
```

#### Syntax Create Collection dengan Validator
```
db.createCollection("collection", {
	validationAction: "error",
	validator: {
		$jsonSchema: {
			// json schema
		}
	}
})
```
E.g.  // Create category collection
```
db.createCollection("merchants",{
	validationAction: "error",
	validator: {
		$jsonSchema: {
			bsonType: "object",
			required: ["name","balance","type","address"],
			properties: {
				name: {
					bsonType: "string",
					description: "Must be a string"
				},
				balance: {
					bsonType: "long",
					description: "Must be a long"
				},
				type: {
					enum: ["PREMIUM","REGULAR"],
					description: "Must be one of the enum values"
				},
				address: {
					bsonType: "object",
					required: ["street","city"],
					properties: {
						street: {
							bsonType: "string",
							description: "Must be a string"
						},
						city: {
							bsonType: "string",
							description: "Must be a string"
						},
						country: {
							bsonType: "string",
							description: "Must be a string"
						}
					}
				}
			}
		}
	}
});
```

// Insert valid document
```
db.merchants.insertOne({
	_id: "toko1",
	name: "toko satu",
	balance: new NumberLong(100000),
	type: "PREMIUM",
	address: {
		street: "Jalan raya satu",
		city: "Jakarta",
		country: "Indonesia"
	}
});
```

// Inser Invalid document: Name is blank
```
db.merchants.insertOne({
	_id: "toko2",
	balance: new NumberLong(100000),
	type: "PREMIUM",
	address: {
		street: "Jalan raya dua",
		city: "Jakarta",
		country: "Indonesia"
	}
});
```
// Inser Invalid document: Address City is blank
```
db.merchants.insertOne({
	_id: "toko2",
	name: "toko dua",
	balance: new NumberLong(100000),
	type: "PREMIUM",
	address: {
		street: "Jalan raya dua",
		country: "Indonesia"
	}
});
```

#### Syntax Update Collection dengan Validator
```
db.runCommand({
	collMod: "collection", // collection modified
	validationAction: "error",
	validator: {
		$jsonSchema: {
			// json schema
		}
	}
})
```
E.g. // Add validator to customers collection
```
db.runCommand({
	collMod: "customers",
	validationAction: "error",
	validator: {
		$jsonSchema: {
			bsonType: "object",
			required: ["full_name"],
			properties: {
				full_name: {
					bsonType: "string",
					description: "Must be a string"
				}
			}
		}
	}
});
```
// Inser Invalid document: Name is blank
```
db.customers.insertOne({
	_id : "kaka",
	name: "kaka"
})
```

Note: data yang sudah terlanjur ada di dalam collection tidak akan hilang / error (tidak di apa-apakan). Tapi jika data baru yang di insert atau data lama di update maka akan divalidasi
