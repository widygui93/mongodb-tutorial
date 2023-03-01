// select * from products order by name asc, category desc

```
db.products.find({}).sort({
    name: 1,
    category: -1
})
```
Note: 
Asc = 1
Desc = -1
