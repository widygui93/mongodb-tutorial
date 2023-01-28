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