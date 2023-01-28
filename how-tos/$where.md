#### Syntax $where operator
```
db.collection.find({
	$where: function(){
		return true;
	}
})
```

Example $where operator
// select * from customers where _id = "widy"
```
db.customers.find({
    $where: function(){
        return this._id == "widy";
    }
});
```

// select * from customers where hex_md5(name) = "b8bba2baae4c2a08fdff4e223458577d"
```
db.customers.find({
	$where: function(){
		return (hex_md5(this.name) == "b8bba2baae4c2a08fdff4e223458577d")
	}
});
```