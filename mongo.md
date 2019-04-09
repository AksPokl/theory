Для хранения данных вместо таблиц - колллекция.
document - это record. Каждый документ является объектом JSON, который хранится внутри BSON.

 - db.createCollection();
 - db.collection.drop();
 
 GridFS is a specification for storing and retrieving files that exceed the BSON-document size limit of 16 MB.
