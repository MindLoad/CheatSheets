---
Title: Mongo
Date: 2024-07-13 20:18
tags:
  - mongo
  - cheatsheet
---
# MongoDB shell [dev]
```bash
mongosh --ssl --host document-dev.cluster.eu-central-1.docdb.amazonaws.com:27017 --sslCAFile global-bundle.pem --username user --password password
```

### DocumentDB manage users 

[Role access/control](https://docs.aws.amazon.com/documentdb/latest/developerguide/role_based_access_control.html)

> [!example]- create user with role
> ```bash
> use admin
> db.createUser({user: "manageruser", pwd: "PaSSword", roles: ["readWrite"]})
> ```
> OR
> ```bash
> db.createUser(
> {
>    user: "manageruser", 
>    pwd: "PaSSword", 
>    roles: []
>})
>
>db.createRole(
>{
>    role: "collectionRole",
>    privileges: [
>    {
>        resource: {db: "translator", collection: "i18n"}, actions: ["find", "update", "insert", "remove"]
>    }],
>    roles: []
>}
>)
> ```
> Grant role to user
> ```bash
> db.grantRolesToUser("user3",["collectionRole"])
> ```
> Revoke role from user
> ```bash
> db.revokeRolesFromUser("manageruser", ["collectionRole"])
> ```


> [!example]- Drop USER
> ```bash
> db.dropUser("manageruser")
> ```

>[!example]- Create collection with schema
>```bash
>db.createCollection("students", {
>  validator: {
>    $jsonSchema: {
>      bsonType: "object",
>      required: ["name", "age"],
>      properties: {
>        name: {
>          bsonType: "string",
>          description: "must be a string and is required"
>        },
>        age: {
>          bsonType: "int",
>          minimum: 0,
>          description: "must be an integer and is required"
>        }
>      }
>    }
>  }
>})
>```

> [!example]- Pagination (from prev. last_id)
> ```python
> def idlimit(page_size, last_id=None):
>	"""Function returns `page_size` number of documents after last_id and the new last_id."""
>	if last_id is None:
>		# When it is first page
>		cursor = db['students'].find().limit(page_size)
>	else:
>		cursor = db['students'].find({'_id': {'$gt': last_id}}).limit(page_size)
>	# Get the data
>	data = [x for x in cursor]
>	if not data:
>		# No documents left
>		return None, None
>	# Since documents are naturally ordered with _id, last document will
>	# have max id.
>	last_id = data[-1]['_id']
>	# Return data and last_id
>	return data, last_id
> ```

### Mongosh commands

| command                                                                                                                                                        | description                                                                                              |     |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | --- |
| show dbs                                                                                                                                                       | show all databases                                                                                       |     |
| show users                                                                                                                                                     | show all available users                                                                                 |     |
| use [database]                                                                                                                                                 | switch to database                                                                                       |     |
| show collections                                                                                                                                               | show all collections                                                                                     |     |
| db.collection.countDocuments({})                                                                                                                               | count all documents in db                                                                                |     |
| db.collection.insertOne({ name: "Alice", age: 25 })<br>db.collection.insertMany([\{ name: "Bob", age: 30 \}, \{ name: "Charlie", age: 35 \}])                  | add one document<br>add many documents                                                                   |     |
| db.collection.find({ age: { $gt: 25 } })<br>db.collection.findOne({ name: "Alice" })<br>db.collection.find({}, {'_id': 1})                                     | Знайти всі документи<br>Знайти і повернути один документ<br>Find all documents and return only _id field |     |
| db.collection.updateOne({ name: "Alice" }, { $set: { age: 26 } })<br>db.collection.updateMany({ age: { $lt: 30 } }, { $inc: { age: 1 } })                      | Оновити один документ<br>Оновити багато документів                                                       |     |
| db.collection.replaceOne({ name: "Alice" }, { name: "Alice", age: 26, city: "New York" })                                                                      | replace document                                                                                         |     |
| db.collection.deleteOne({ name: "Alice" })<br>db.collection.deleteMany({ age: { $lt: 30 } })                                                                   | Delete one document<br>Delete many documents                                                             |     |
| db.collection.aggregate([<br>  { \$match: { status: "active" } },<br>  { \$group: { _id: "$status", total: { $sum: 1 } } }<br>])                               | Basic aggregation                                                                                        |     |
| db.collection.aggregate([<br>  { $match: { age: { $gt: 25 } } },<br>  { $sort: { age: 1 } },<br>  { $limit: 10 },<br>  { $project: { name: 1, age: 1 } }<br>]) | Pipeline stages                                                                                          |     |
| db.collection.createIndex({ name: 1 })<br>db.collection.createIndex({ age: -1 })                                                                               | create index                                                                                             |     |
| db.collection.getIndexes()                                                                                                                                     | view indexes                                                                                             |     |
| db.collection.dropIndex("name_1")                                                                                                                              | drop index                                                                                               |     |
| db.serverStatus()                                                                                                                                              | view server status                                                                                       |     |
| db.collection.stats()                                                                                                                                          | get collection stats                                                                                     |     |
| db.collection.drop()                                                                                                                                           | drop collection                                                                                          |     |
| db.dropDatabase()                                                                                                                                              | drop database                                                                                            |     |
| db.translator_collection.find({'_id': {'$gt': 1142}}).limit(2)                                                                                                 | Pagination by last_id from previous                                                                      |     |
|                                                                                                                                                                |                                                                                                          |     |
### Mongosh transaction

| command                                                                                                                                                         | description                       |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| session = db.getMongo().startSession()<br>session.startTransaction()                                                                                            | Start transaction                 |
| session.getDatabase('test').collection.insertOne({ name: "Alice" })<br>session.getDatabase('test').collection.updateOne({ name: "Bob" }, { $set: { age: 31 } }) | Perform operations in transaction |
| session.commitTransaction()<br>session.endSession()                                                                                                             | Commit transaction                |
| session.abortTransaction()<br>session.endSession()                                                                                                              | Abort transaction                 |
|                                                                                                                                                                 |                                   |
### Pymongo commands

```python
client = MongoClient("mongodb://localhost:27017/")
db = client['your_database_name']
collection = db['your_collection_name']
```

| command                                                                      | description                         |
| ---------------------------------------------------------------------------- | ----------------------------------- |
| collection.replace_one({"_id": 1}, {"_id": 1, "field": "text"}, upsert=True) | Replace existed or Add new document |
|                                                                              |                                     |
