| Operator | Description |
| --- | ---- |
| $and | Menggabungkan query dengan operasi AND, mengembalikan document jika semua kondisi benar|
| $or | Menggabungkan query dengan operasi OR, mengembalikan document jika salah satu kondisi benar |
| $nor | Menggabungkan query dengan operasi NOR, mengembalikan document yang gagal di semua kondisi |
| $not | Membalikkan kondisi, mengembalikan document yang tidak sesuai kondisi|

Syntax $and, $or, $nor 

```
db.collection.find({
	$operator : [
		{
			// expression
		},
		{
			// expression
		}
	]
})
```

e.g:

// select * from products where category in ('laptop', 'handphone') and price > 2000000
```
db.products.find({
    $and: [
        {
            category: {
                $in: ["laptop", "handphone"]
            }
        },
        {
            price: {
                $gt: 20000000
            }
        }
    ]
});
```

// select * from products where price between 10000000 and 20000000 and category != 'food'
```
db.products.find({
	$and: [
		{
			$and: [
				{
					price: {
						$gte: 10000000
					}
				},
				{
					price: {
						$lte: 20000000
					}
				}
			]
		},
		{
			category:{
				$ne: "food"
			}
		}
	]
})
```

or
```
db.products.find({
    $and: [
        {
            price: {
                $gte: 10000000,
                $lte: 20000000
            }
        },
        {
            category: {
                $ne: 'food'
            }
        }
    ]
});
```

Syntax $not
```
db.collection.find({
	field: {
		$not: {
			// operator expression
		}
	}
})
```

e.g:

// select * from products where category not in ('laptop','handphone')
```
db.products.find({
	category: {
		$not: {
			$in: ['laptop','handphone']
		}
	}
})
```