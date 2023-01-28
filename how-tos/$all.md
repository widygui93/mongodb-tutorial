#### Syntax $all operator
```
db.collection.find({
	field: {
		$all: ["value"]
	}
});
```

#### example $all operator
// select * from products where (tags = "samsung" and tags = "monitor")
```
db.products.find({
    tags: {
        $all: ["samsung","monitor"]
    }
});
```

#### Equivalent to $and from [[Logical Query Operator]]
```
db.products.find({
    $and : [
        {
            tags: "samsung"
        },
        {
            tags: "monitor"
        }
    ]
});
```

#### Use $all with [[ $elemMatch]]
If the field contains an array of documents, we can use the $all with the $elemMatch operator.

The following operation queries the `inventory` collection for documents where the value of the `qty` field is an array whose elements match the [`$elemMatch`](https://www.mongodb.com/docs/manual/reference/operator/query/elemMatch/#mongodb-query-op.-elemMatch) criteria

```
db.inventory.find({
    qty: {
        $all: [
            {"$elemMatch" : { size: "M", num: { $gt: 50}}},
            {"$elemMatch" : { num: 100,color: "green"}}
        ]
    }
});
```
