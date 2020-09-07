# M001 Mongo DB Basics

## Chapter 0 Setup

- Tools: Compass(visual interface), Atlas(DB as a Service), shell
- start the mongo shell using the following command in the prompt in win, without connecting to any instances of the db
  `mongo --nodb`
- For installing mongodb in other OS, refer the docs in the download center
- Atlas:
  - DB as a service solution
  - replication is handled
  - clusters can be deployed
  - use the free tier for this course, no expiry date
  - look for other services provided by mongodb: like Data Explorer, charts, stitch, etc

## Chapter 1 Introduction

- JSON - JavaScript Object Notation
- suppoted data types are string, number, object, array, boolean, null
- Databases, collections and documents(each contains the following stuff)
- the above three in combinations creates a namaspace
- Scalar Value Types <https://youtu.be/N4E3TBHul0w>
- Aggregate Value Types - Fields with Documents as Values <https://youtu.be/KM_GMvAinG8>
- Aggregate Value Types - Fields with Arrays as Values <https://youtu.be/gz3Hpd_Sl9U>
- Aggregate Value Types - Geospatial Data <https://youtu.be/hgPuNdCZfAw>
- Filtering Collections with Queries <https://youtu.be/R6RKfhpHfd8>
  - schema in compass gui, lets you see visibly the data and their info
  - geo data can be viewed as well
  - any selection of types of data automatically makes an equality filter
  - `$gte`, `$lt` are operators in mongodb
- CRUD - Create, Read, Update, Delete

## Chapter 2 The mongo DB Query Language + Atlas

- Create a new free atlas cluster
- Create and connect to a sandbox cluster
- check the handouts in the chapter2 folder
- Connect to the sandbox from both shell and compass
- do CRUD in compass db: `insertOne`, use dbname, show collections,
- `_id` is unique inside a single collection, and auto inserted
- insertMany: to do bulk insert into the db
- docs throwing error in insertMany will have to habdled using the second arg, `{"ordered":false}`. This avoids inserting the document in the normal order
- quality filters: `{"key1.key2":"value" }` key2 is required in some cases
- exact matches for array fields: `{"key1":["value", "value2"]}`
- `db.movies.find({key.position: "value"}).pretty()`
- iterating over the results is possible. type 'it' in shell to move around the search results.
- mongodb returns all fields bu default after a search. Provide a second arugment as what you want to be displayed in the results `{title: 1}` to be included, `{title:1, "_id":0}` for `_id` field not to be displayed
- `updateOne()`: we update one document in mongodb, `db.movieDetails.updateOne({title: "The Martian"}, {$set:{poster:"something"}})`. This example uses the `$set` operator
- results of updateOne will be the number of documents updated
- Update operators: `$unset, $min, $max, $push` are some examples of other remaining update operators. <https://docs.mongodb.com/manual/reference/operator/update/>
- `updateMany`: `db.movieDetails.updateMany({"rated":null}, {$unset:{rated: ""}})`
- upsert: replace if the conditon is matched or insert a new document
- `replaceOne`: `let filter={"title": "House, M.D., Season Four: New Beginnings"}; let doc = db.movieDetails.findOne(filter); doc.genres.push("TV Series"); doc.poster="something"; db.movieDetails.replaceOne(filter, doc);`
- By default, the above code will replace only the first document matching the filter condition
- `deleteOne, deleteMany`: send a condition based on which a document should be deleted
- load the movie reviews collection into the sandbox, login using `mongo MONGO_URL`, then run the command `load(JS_FILE_NAME)`

## Chapter 3 Deeper Dive into MongoDB Query Language

- CRUD can be operated upon using the query operators in the mongodb
- comparison query operators: `db.movieDetails.find({runtime:{$gte: 90, $lte: 120}}, {title:1, _id:0}).count()`
- some operators are `$gt, $gte, $lt, $lte, $ne, $in, $nin`
- Element (values check) operators: `$exists, $type`
- used mainly when searching for null values but the code returns even the missing field documents
- `db.movies.find({viewerRating: {$type: "int"}}).pretty()`
- `{atmosphericPressureChange: {$exists: false}}` - to find if the field exists or not
- Logical operators; `$and, $not, $nor, $or`, selectors are in the following syntax.
- `{$or: [{watlev:{$eq: 'always dry'}}, {depth: {$eq: 0} }]}`
- `$all` - matches an array of elements and should match completely but not in the same order
- `{sections: {$all: ["AG1", "MD1", "OA1"]}}`
- `$size`- syntax similar to `$all`, allows you to select the results based on the counts
- `{sections: {$size: 2}}`
- `$elemMatch` - TODO aagin <https://youtu.be/e21qIIy9rxk>
- `use results`
- `db.scores.find({results: {$elemMatch: {$gte: 70, $lt: 80}}}).count()`
- `{results: {$elemMatch: {product: "abc", score: 7}}}`
- NOTE: the mogodb shell is a JS interpreter
- `$regex` operator: similar to usage with `$size`
