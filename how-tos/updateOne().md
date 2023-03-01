#### Syntax upateOne() Function
```
db.collection.updateOne(
	{}, // filter
	{}, // update
	{}  // option
)
```
#### Example updateOne() Function
// update products set category = "food" where _id = 1
```
db.products.updateOne(
	{ _id: 1 },
	{
		$set: {
			category: "food"
		}
	}
);
```

Specify an empty filter to update the first document returned in the collection.
```
db.products.updateOne(
	{},
	{
		$set: {
			category: "food"
		}
	}
);
```

When `upsert` is `true` , the `updateOne()` etiher:
* Create a new document if no documents match the `filter`
* Update a single document that match the `filter`
```
db.customers.updateOne(
	{ _id: 2},
	{
		$set: {
			name: "susi"
		}
	},
	{ upsert: true }
);
```
Default is `false`, which does not insert a new document when no match is found.

#### Update with Aggregation Pipeline
* Add the new `comments` field and set the `lastUpdate` field and `status`
* Remove the `misc1` and `misc2` fields for all the documents in the collection

```
db.members.updateOne(
	{ _id: 1 },
	[
		{ $set: { status: "Modified", comments: ["$misc1", "$misc2"],lastUpdate: "$$NOW" } },
		{ $unset: ["misc1", "misc2"] }
	]
);
```
Reference: [Doc](https://www.mongodb.com/docs/manual/reference/method/db.collection.updateOne/#example-1)

#### Update with `arrayFilters`
```
db.students.updateOne(
	{ grades: { $gte: 100 }},
	{ $set: { "grades.$[element]": 100 }},
	{ arrayFilters: [ {"element": { $gte: 100 } } ] }
);
```