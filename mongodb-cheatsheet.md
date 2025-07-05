MongoDB follows a document-based (NoSQL) structure, where data is stored in JSON-like documents.

Key MongoDB Characteristics:
* Schema-less (documents can have different fields)
* Hierarchical data supported natively (nested documents)
* Collections do not enforce structure (flexible)
* Uses BSON format internally (Binary JSON)



Switch to or create a new DB:

Use testdb

to check you are inside which db:

db


Insert a document:

db.user.insertOne({name:’Mahesh’, role: ‘developer, skills: [‘Python’, ‘Java’]’})


View the inserted document:

db.collectionName.find()

See all collections in your DB:

show collections

See all your databases :
show dbs

drop database: 

db.dropDatabase()

Drop a Specific Collection

db.collectionName.drop()


Delete All Documents from a Collection (but keep the collection structure):-

db.users.deleteMany({})


db.post.countDocuments(): -

Returns the exact number of documents in the collection (or matching a filter).
Internally performs a collection scan to count documents.


db.post.estimatedDocumentCount(): -

Returns an estimated total number of documents in a collection.
It is much faster than countDocuments() because it uses collection metadata rather than scanning documents.


db.post.find().limit(3): -

will return the first 3 documents from the post collection.

creating collection : 
db.createCollection(‘collectionName’)


db.post.insert({
	title: ‘post collection’,
	body: ‘body of post’,
	category: [‘post’, ’events’],
	user: {
		name: ‘Mahesh’,
		status: ‘Active’	
	},
	date: date()
})




insertMany collection: -


db.post.insertMany([
  {
    title: 'Post One',
    body: 'This is the first post',
    category: ['news', 'tech'],
    user: {
      name: 'Mahesh',
      status: 'Active'
    },
    date: new Date()
  },
  {
    title: 'Post Two',
    body: 'Second post content goes here',
    category: ['events', 'community'],
    user: {
      name: 'Aarav',
      status: 'Inactive'
    },
    date: new Date()
  },
  {
    title: 'Post Three',
    body: 'Third post content',
    category: ['updates'],
    user: {
      name: 'Sia',
      status: 'Active'
    },
    date: new Date()
  }
])

pretty () — >. can be used with only find() not findOne();


updateOne: -

Update the title of the post where user.name is "Mahesh":

db.post.updateOne(
	{ "user.name": "Mahesh" },         // filter
  	{ $set: { title: "Updated Title" } }  // update
)

Update the status of all users to "Inactive" where category contains "events":
$set operator is used to add a new field or update the value of an existing field in a document.

db.updateMany(
	{category: ‘events’},
	{$set: {‘user.status’: ‘Inactive’}}
)


rename function:- rename for one field 

db.post.updateOne(
  { title: "Post One" },
  { $rename: { "title": "post_title" } }
)



delete: - 

db.post.deleteOne({ title: 'Post Three' })
db.post.delete({ title: 'Post Three' }) —X not valid 


Operation	Syntax
Delete one document	db.post.deleteOne({ title: 'Post Three' })
Delete many documents	db.post.deleteMany({ category: 'events' })
Drop entire collection	db.post.drop()


Find By Element in Array ($elemMatch): -

db.posts.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)

alternative:   db.post.find({
  "comments.user": "Mary Williams"
})


Indexes: -
create index: 

db.collectIonName.createIndex({field: ‘index_name’})

to view all the index in that particular  collection:

db.collectName.getIndexes()


dropping an index: - 
db.post.dropIndex("title_text")
