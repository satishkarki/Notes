

MongoDB is a document-oriented `NoSQL` database used for  high volume data storage. Instead of using tables and rows as in the  traditional relational databases, MongoDB makes use of collections and  documents. Documents consist of `key-value` pairs which are the basic unit of data in MongoDB. Collections contain sets of documents and function  which is the equivalent of relational database tables.

## Installation

This installation guide is for MongoDB 5.0 Community Edition.  

**Step 1**: Importing the MongoDB public GPG Key

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
```

**Step 2**: Creating a list file for MongoDB

```bash
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
```

**Step 3**: Reload local package database

```bash
sudo apt-get update
```

**Step 4**: Install the MongoDB packages

```bash
#Installs the latest version of MongoDB
sudo apt-get install -y mongodb-org
```

Note: apt-get will upgrade the packages when a new version becomes available. To prevent unintended upgrades we can pin the packages at the currently installed version.

```bash
echo "mongodb-org hold" | sudo dpkg --set-selections
echo "mongodb-org-database hold" | sudo dpkg --set-selections
echo "mongodb-org-server hold" | sudo dpkg --set-selections
echo "mongodb-org-shell hold" | sudo dpkg --set-selections
echo "mongodb-org-mongos hold" | sudo dpkg --set-selections
echo "mongodb-org-tools hold" | sudo dpkg --set-selections
```

## Run MongoDB Community Edition

**Step 1**: Start MongoDB

```bash
sudo systemctl start mongod

# If you receive an error like this use the command below
# Failed to start mongod.service: Unit mongod.service not found.

sudo systemctl daemon-reload
```

**Step 2**: Verify MongoDB has started

```bash
sudo systemctl status mongod

# You can optionally ensure that MongoDB will start following a system reboot by issuing the following command:
sudo systemctl enable mongod
```

If you want to stop MongoDB

```bash
sudo systemctl stop mongod

# To check the log
/var/log/mongodb/mongod.log
```

**Step 3**: begin Using MongoDB

```bash
mongosh
```

## CRUD Operation

### CREATE

```shell
 # show dbs
admin     41 kB
config  36.9 kB
local     41 kB

 # use shopDB
switched to db shopDB

# db
shopDB

# db.products.insertOne({_id:1,name:"pen",price:1.20})
{ acknowledged: true, insertedId: 1 }

# show collections
products
```

### READ

```bash
# shopDb> db.products.find()
[
  { _id: 1, name: 'pen', price: 1.2 },
  { _id: 2, name: 'pencil', price: 1.8 }
]

# shopDb> db.products.find({name:"pencil"})
[ { _id: 2, name: 'pencil', price: 1.8 } ]

# shopDb> db.products.find({price:{$gt:1}})
[
  { _id: 1, name: 'pen', price: 1.2 },
  { _id: 2, name: 'pencil', price: 1.8 }
]

# shopDb> db.products.find({_id:1},{name:1})
[ { _id: 1, name: 'pen' } ]

# shopDb> db.products.find({_id:1},{name:1, _id:0})
[ { name: 'pen' } ]
```

### UPDATE

```bash
# shopDb> db.products.updateOne({_id:1},{$set:{stock:32}})
 {
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

# shopDb> db.products.find()
[
  { _id: 1, name: 'pen', price: 1.2, stock: 32 },
  { _id: 2, name: 'pencil', price: 1.8 }
]

```

### DELETE

```bash
 # shopDb> db.products.deleteOne({_id:2})
{ acknowledged: true, deletedCount: 1 }

```

## [mongoDB and node.js](https://docs.mongodb.com/drivers/node/current/)

![Mongo](mongo.png)

```bash
npn install mongodb 
```

```javascript
// For Node.js Version 4.1

const { MongoClient } = require("mongodb");
// Connection URI
const uri =
  "mongodb+srv://sample-hostname:27017/?poolSize=20&writeConcern=majority";
// Create a new MongoClient
const client = new MongoClient(uri);
async function run() {
  try {
    // Connect the client to the server
    await client.connect();
    // Establish and verify connection
    await client.db("admin").command({ ping: 1 });
    console.log("Connected successfully to server");
  } finally {
    // Ensures that the client will close when you finish/error
    await client.close();
  }
}
run().catch(console.dir);
```

[Documentation](https://docs.mongodb.com/drivers/node/current/fundamentals/connection/)

Kill the mongodb server

```bash
sudo pkill -f mongod
```

### Connecting MongoDB Atlas to Shell

```shell
mongosh "mongodb+srv://blogcluster.qa8ys.mongodb.net/myFirstDatabase" --username *******
```

### Connecting MongoDB Atlas to Application

```javascript
// Full Driver Code
const { MongoClient } = require('mongodb');
const uri = "mongodb+srv://butcher:<password>@blogcluster.qa8ys.mongodb.net/myFirstDatabase?retryWrites=true&w=majority";
const client = new MongoClient(uri, { useNewUrlParser: true, useUnifiedTopology: true });
client.connect(err => {
  const collection = client.db("test").collection("devices");
  // perform actions on the collection object
  client.close();
});
```

Instead of writing this large block of code, we can use mongoose which will handle everything for us in the back.

```javascript
const mongoose=require("mongoose");
mongoose.connect("mongodb+srv://butcher:<password>@blogcluster.qa8ys.mongodb.net/myFirstDatabase?retryWrites=true&w=majority");
```

### Mongoose Schema

```javascript
const <schemaName>={
    <fieldName>:<FieldDataType>,
    ....
}
//Example
const itemSchema={
    name:String
};
```

### Mongoose Model

```javascript
const <Name>=mongoose.model(
<"SingularCollectionName">,
<schemaName>
)
// Example
const Item=mongoose.model("Item", itemSchema);
```

### Mongoose Document

```javascript
const <constantName>=new <ModelName>({
<fieldName>:<fieldData>,
....
})
//Example
const item1=new Item({
    name: "Welcome to your todolist"
});
```

### Mongoose insertMany()

```javascript
<ModelName>.insertMany(<documentArray>, function(err){
//Deal with the error or log success.
});

//Example
Item.insertMany(defaultItems, function(err){
    if(err){
        console.log(err);
    } else{
        console.log("Successfully saved default items to DB.");
    }
});
```

### Mongoose find()

```javascript
<ModelName>.find({conditions},function(err, results){
// Use the found results docs
});
//Example
   Item.find({},function(err, foundItems){
        res.render("list",{listTitle:day, newListItems:foundItems});
    })
```

### Mongoose findByIdAndRemove()

```javascript
<ModelName>.findByIdAndRemove(<Id>,function(err){
//Handle any errors or log success.
});

```

### Mongoose findOne()

```javascript
<ModelName>.find({conditons}, function(err,results){
//Use the found results docs.
});
```

### Mongoose findOneAndUpdate()

```javascript
<ModelName>.findOneAndUpdate(
{conditions}
{updates},
function(err,results){}
);


<ModelName>.findOneAndUpdate(
{conditions}
{$pull:{field:{_id:}}},
function(err,results){}
);
```



## References

https://docs.mongodb.com/

https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/

https://docs.mongodb.com/manual/tutorial/getting-started/

https://docs.mongodb.com/drivers/node/current/fundamentals/connection/

https://mongoosejs.com/

https://www.guru99.com/what-is-mongodb.html