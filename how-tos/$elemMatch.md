#### Syntax $elemMatch operator
```
db.collection.find({
	fields: {
		$elemMatch: {
			// query 1,
			// query 2
		}
	}
})
```
#### Syntax $elemMatch operator sebagai projections
```
db.collection.find({},{
	field: {
		$elemMatch: {
			// query
		}
	}
})
```

#### example $elemMatch operator
// select * from products where tags in ("samsung", "logitect")
```
db.products.find({
    tags: {
        $elemMatch: {
            $in: ["samsung","logitech"]
        }
    }
});
```
note: We cannot use [[$where]] and [[$text]] in $elemMatch

#### Element Match
```
db.scores.find(
   { results: { $elemMatch: { $gte: 80, $lt: 85 } } }
)
```
#### More than one condition query
```
db.survey.find(
   { results: { $elemMatch: { product: "xyz", score: { $gte: 8 } } } }
)
```

// select _id, name, category, price, tags(in ("samsung", "logitech")) from products
```
db.products.find({}, {
	name: 1,
	category: 1,
	price: 1,
	tags: {
		$elemMatch: {
			$in: ["samsung","logitech"]
		}
	}
});
```