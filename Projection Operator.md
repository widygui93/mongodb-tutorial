* Pada function `find` terdapat parameter kedua setelah query, yaitu `projection`
* `Projection` adalah memilih field mana yang ingin kita include atau exclude

#### Syntax projection
```
db.<collection>.find({
	// query,
},{
	field1: 1 // include,
	field2: 0 // exclude
});
```

| Operator | Keterangan |
| --- | ------------- |
| [[$]] | Limit array hanya mengembalikan data pertama yang match dengan array operator |
| [[$elemMatch]] | Limit array hanya mengembalikan data pertama yang match dengan kondisi query |
| [[$meta]] | Mengembalikan informasi metadata yang didapat dari setiap matching document |
| [[$slice]] | Mengontrol jumlah data yang ditampilkan pada array |

