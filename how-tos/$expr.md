#### Syntax $expr operator
```
db.collection.find({
	$expr: {
		// aggregation expression
	}
})
```

example $expr operator
// select * from products where price > 1000000
```
db.products.find({
    $expr: {
        $gt: ["$price", 1000000]
    }
});
```

or 
// select * from monthlyBudget where spent > budget
```
db.monthlyBudget.find({ 
	$expr: { 
		$gt: [ "$spent" , "$budget" ] 
	} 
});
```

or
// select *  from customers where toUpper(_id) = 'KHANNEDY'
```
db.customers.find({
    $expr: {
        $eq: [ { $toUpper: "$_id" }, "KHANNEDY" ]
    }
});
```

