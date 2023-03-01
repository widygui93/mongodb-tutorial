// select * from products offset 2
```
db.products.find({}).skip(2)
```
// select * from products limit 4 offset 2
```
db.products.find({}).limit(4).skip(2)
```
equal result with
```
db.products.find({}).skip(2).limit(4)
```
