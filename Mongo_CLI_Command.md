## MongoDB


In mongoDB a table is called "**Collection**"

To connect to mongo shell (in our mongodb docker container) from git bash:
````shell
docker exec -it mongo-dev bash

  # Old version
mongo

  # Mongodb version 6
mongosh

  # Admin access
mongosh -u root -p pwd
````
---
#### CLI Command

1. Show, find and count

````shell
show dbs

use mydb   # use or create database

show collections

db.mytest.find().pretty()

db.mytest.find().limit(5).pretty()

db.mytest.find({}, {name:1, price:1, rating:1}).limit(5)

db.mytest.find({}, {name:1, price:1, _id:0})

  # find Name:
db.mytest.find({type:'accessory'})

  # find all name that contain specific worlds:
db.mytest.find({type:/case/})

  # find all name that contain specific worlds & case sensitive:
db.mytest.find({type:/case/i})

  # Count:
db.mytest.find({name:/ac3/i}).count()

````
2. Insertion, drop

````shell
  # Insert One:
db.mytest.insertOne({name:'Fr', location:{country:'FR', city:'Paris'}})

  # Insert Many:
db.mytest.insertMany({{model:'Peugeot', price:'16500'}, {model:'Alfa Romeo', price:'24000'}})

  # Drop Collection:
db.mytest.drop()

  # Drop Database:
db.dropDatabase()

  # Loop to insert many values:
for(let i=0; i<10; i++) {
  ... db.mytest.insert({nom:'My ID num ${i}'});}
````
3. Find greater then, less then, equal, and, or & in:
````shell
  # find greater then:
db.mytest.find({price:{$gt:20}})

  # find greater then and equal:
db.mytest.find({price:{$gte:20}})

  # find less then:
db.mytest.find({price:{$lt:60}})

  # find less then and equal:
db.mytest.find({price:{$lte:20}})

  # find OR and AND:
db.mytest.find({$or:[{rating:4}, {rating:3.9}]}})

db.mytest.find({$and:[{rating:4}, {price:1200}]}})

  # find Equal:
db.mytest.find({'limits.data.over_rate':{$eq:0}})

  # find IN:
db.mytest.find({'limits.data.over_rate':{$in:[0,1]}})

  # find NOT IN:
db.mytest.find({'limits.data.over_rate':{$nin:[0,1]}})

  # find NOT EQUAL:
db.mytest.find({'limits.data.over_rate':{$ne:0}})

  # find ALL:
db.mytest.find({for:{$all:['ac3', 'ac7']}})
````
4. Insert, Update, Rename, Add
````shell
  # Update:
db.mytest.updateOne({name:'Jean'}, {$set:{name:'Jean Luc'}})

db.mytest.updateOne({name:'Jean'}, {$set:{'location.city':'Paris'}})

  # Update by adding new items (exemple= province inside city):
db.mytest.updateOne({name:'Jean'}, {$set:{'location.city': {ville:'Paris', province:'Île-de-France'}}})

  # Rename the name of item:
db.mytest.updateOne({name:'Jean'}, {$rename:{'location.city.city': 'location.city.ville'}})

  # Add an item(should be inside an array):
db.mytest.updateOne({name:'Jean'}, {$push:{'location.city': 'saint-denice'}})
````
5. Delete
````shell
db.mytest.deleteOne({name:'David'})

db.mytest.remove({_id:ObjectId("63c551f154re5f7b")})
````
6. Sort, skip
````shell
  # Sort
db.mytest.find().sort({price: 1})  # 1: ascending order

db.mytest.find().sort({price: -1})  # -1: descending order

db.mytest.find().sort({price: -1, rating: 1})

  # Skip
db.mytest.find().skip(2).limit(10)
````
7. Aggregation
````shell
  # Group By
db.mytest.aggregate([{$group: {_id:'$type', nomber:{$sum:1}}}])

  # Distinct
db.mytest.distinct('Type')

  # Join
constemploi = db.client.findOne({'nom': 'Thuiller'})
db.emploi.insertMany([{'emploi': 'Jardinier', 'nomid': constemploi._id}])
````
8. set, push, pull
````shell
  # $set: replace value
  # $push: append a specific value to an array
  # $pull: remove value from an array
````
