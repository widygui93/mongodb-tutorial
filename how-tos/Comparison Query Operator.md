| Operator | Description |
| ------ | ------- |
| $eq | Membandingkan value dengan value lain |
| $gt | Membandingkan value lebih besar dari value lain |
| $gte | Membandingkan value lebih besar atau sama dengan value lain |
| $lt | Membandingkan value lebih kecil dari value lain |
| $lte | Membandingkan value lebih kecil atau sama dengan value lain |
| $in | Membandingkan value dengan value yang ada di array |
| $nin (not in) | Membandingkan value tidak ada dalam value yang ada di array |
| $ne (not equal) | Membandingkan value tidak sama dengan value lain |

Syntax:

```
db.customers.find({
	field: {
		$operator: "value"
	}
})
```

e.g:

// select * from customers where _id = "widy"

```
db.customers.find({
	_id: {
		$eq: "widy"
	}
})
```

// select * from products where category in ('handphone', 'laptop') and price > 5000000

```
db.products.find({
    category: {
        $in: ["handphone", "laptop"]
    },
    price: {
        $gt: 5000000
    }
});
```
