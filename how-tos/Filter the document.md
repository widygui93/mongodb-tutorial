```
db.customers.find({city: "New York"})
```

// select * from orders where items.product_id = 1

```
db.orders.find({
    "items.product_id": 1
});
```

// select * from customers where _id = "widy" and name = "widy guilias"
```
db.customers.find({
	_id: "widy", 
	name: "widy guilias"

})
```