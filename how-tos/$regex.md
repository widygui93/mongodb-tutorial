#### Syntax $regex operator
```
db.collection.find({
	field: {
		$regex: /regex/,
		$options: "<option>"
	}
})
```

OR

```
db.collection.find({
	field: {
		$regex: /regex/<option>
	}
})
```

Example $regex operator
// select * from products where name like "%mie%"
```
db.products.find({
    name: {
        $regex: /mie/,
        $options: "i"
    }
});
```

OR 
```
db.products.find({
    name: {
        $regex: /mie/i
    }
});
```

// select * from products where name like "Mie%"
```
db.products.find({
    name: {
        $regex: /^Mie/
    }
});
```

// select * from products where category in (/^lap/ , /phone$/)
```
db.products.find({
    category: {
        $in: [/^lap/, /phone$/ ]
    }
});
```
**Note**: You can't use $regex operator inside $in operator

// select * from name like "%mie%" and name not in ("masker","tissue")
```
db.products.find({
	name: {
		$regex: /mie/i,
		$nin: ["masker","tissue"]
	}
});
```

The regular expression "(?i)a(?-i)cme" match string that:
* Begin with "a" or "A". This is a case-insensitive match.
* End with "cme" . This is a case-sensitive match.

```
db.products.find({
	name: {
		$regex: "(?i)a(?-i)cme"
	}
});
```



