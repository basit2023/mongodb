 # MongoDB Query Guide for Beginners

This guide will help you get started with MongoDB queries. MongoDB is a NoSQL database that stores data in flexible, JSON-like documents. Below are the basic commands and examples to interact with a MongoDB database.

---
Here’s a simple explanation of **what a database is** and **what MongoDB is**, designed for teaching beginners:

---

### **What is a Database?**

A **database** is an organized collection of data that can be easily accessed, managed, and updated. Think of it as a digital filing system where data is stored and retrieved efficiently.

- **Why Do We Use a Database?**
  - To store large amounts of data in a structured way.
  - To quickly retrieve and manipulate data.
  - To keep data organized and avoid duplication.

#### **Types of Databases**
1. **Relational Databases (SQL)**:
   - Data is stored in tables with rows and columns (like Excel).
   - Examples: MySQL, PostgreSQL, SQLite.

2. **Non-Relational Databases (NoSQL)**:
   - Data is stored in flexible formats like JSON, documents, or key-value pairs.
   - Examples: MongoDB, Cassandra, DynamoDB.

---

### **What is MongoDB?**

MongoDB is a **NoSQL database** that stores data in a flexible, JSON-like format called **documents**. It’s designed to handle unstructured or semi-structured data and is perfect for modern applications that need to scale quickly.

#### **Key Features of MongoDB**
1. **Document-Oriented**:
   - Instead of tables and rows, MongoDB uses **collections** and **documents**.
   - Documents are similar to JSON objects and allow flexible data structures.

2. **Scalable**:
   - MongoDB can handle large amounts of data and traffic by distributing data across multiple servers (horizontal scaling).

3. **Schema-less**:
   - You don’t need to define the structure of your data in advance. Each document can have a different structure.

4. **High Performance**:
   - Fast reads and writes, making it ideal for applications with high demands for speed.

#### **How MongoDB Stores Data**
- **Database**: The highest level, like a folder that contains data.
- **Collection**: A group of documents (like a table in SQL).
- **Document**: A single record, stored in JSON format.

Example of a MongoDB document:
```json
{
  "name": "intern",
  "age": 25,
  "city": "isb",
  "skills": ["JavaScript", "React", "Node.js"]
}
```

---

### **Why Choose MongoDB?**

- **Flexibility**: No predefined schema; great for rapidly changing projects.
- **Ease of Use**: Data is stored in JSON-like documents, which is developer-friendly.
- **Speed**: Handles queries and writes very efficiently.
- **Scalability**: Can grow with your application by adding more servers.

---

### **Real-World Use Cases of MongoDB**
1. **E-Commerce Applications**: Storing product catalogs with different attributes.
2. **Social Media Platforms**: Storing user profiles, posts, and comments.
3. **Real-Time Analytics**: Monitoring and analyzing live data.
4. **Content Management Systems (CMS)**: Managing and delivering content like articles or videos.

---

### **Analogy for Beginners**

- Think of a **database** as a library.
- The **collections** in MongoDB are like sections of the library (e.g., Fiction, Science, History).
- The **documents** are like the books within those sections, with each book (document) containing specific information.

---


## Prerequisites

1. **MongoDB Installed**: Install MongoDB on your system. Refer to the [MongoDB Installation Guide](https://www.mongodb.com/docs/manual/installation/).
2. **Mongo Shell or Compass**: Use either Mongo Shell (CLI) or MongoDB Compass (GUI) to execute queries.
3. **Basic Setup**: A database and collection to practice with (e.g., `myDatabase` and `myCollection`).

---

## Basic MongoDB Commands

### 1. **Connect to MongoDB**
```bash
mongo
```

### 2. **Show All Databases**
```bash
show dbs
```

### 3. **Switch or Create a Database**
```bash
use myDatabase
```

### 4. **Create a Collection**
```javascript
db.createCollection("myCollection")
```

### 5. **Show Collections**
```javascript
show collections
```

---

## CRUD Operations

### 1. **Insert Documents**
Add a single document:
```javascript
db.myCollection.insertOne({ name: "Alice", age: 25, city: "New York" })
```

Add multiple documents:
```javascript
db.myCollection.insertMany([
  { name: "Bob", age: 30, city: "Chicago" },
  { name: "Charlie", age: 35, city: "San Francisco" }
])
```

### 2. **Read (Query) Documents**
Retrieve all documents:
```javascript
db.myCollection.find()
```

Retrieve documents with a filter:
```javascript
db.myCollection.find({ age: { $gt: 25 } })
```

Format the output (pretty print):
```javascript
db.myCollection.find().pretty()
```

### 3. **Update Documents**
Update a single document:
```javascript
db.myCollection.updateOne(
  { name: "Alice" }, 
  { $set: { age: 26 } }
)
```

Update multiple documents:
```javascript
db.myCollection.updateMany(
  { city: "Chicago" }, 
  { $set: { state: "Illinois" } }
)
```

### 4. **Delete Documents**
Delete a single document:
```javascript
db.myCollection.deleteOne({ name: "Alice" })
```

Delete multiple documents:
```javascript
db.myCollection.deleteMany({ age: { $lt: 30 } })
```

---

## Query Operators

### Comparison Operators
- `$eq` – Equals: `{ age: { $eq: 25 } }`
- `$ne` – Not equal: `{ age: { $ne: 25 } }`
- `$gt` – Greater than: `{ age: { $gt: 25 } }`
- `$gte` – Greater than or equal: `{ age: { $gte: 25 } }`
- `$lt` – Less than: `{ age: { $lt: 25 } }`
- `$lte` – Less than or equal: `{ age: { $lte: 25 } }`

### Logical Operators
- `$and` – AND: `{ $and: [{ age: { $gt: 25 } }, { city: "New York" }] }`
- `$or` – OR: `{ $or: [{ age: { $lt: 25 } }, { city: "Chicago" }] }`
- `$not` – NOT: `{ age: { $not: { $gt: 25 } } }`


### **1. `$and` – Logical AND**

#### Syntax:
```javascript
db.collection.find({
  $and: [
    { <field1>: <condition1> },
    { <field2>: <condition2> }
  ]
})
```

#### Example:
Find documents where:
- Age is greater than 25 **AND**
- City is "New York".

```javascript
db.collection.find({
  $and: [
    { age: { $gt: 25 } },
    { city: "New York" }
  ]
})
```

#### Example Document Match:
```json
{
  "name": "Alice",
  "age": 30,
  "city": "New York"
}
```

---

### **2. `$or` – Logical OR**

#### Syntax:
```javascript
db.collection.find({
  $or: [
    { <field1>: <condition1> },
    { <field2>: <condition2> }
  ]
})
```

#### Example:
Find documents where:
- Age is less than 25 **OR**
- City is "Chicago".

```javascript
db.collection.find({
  $or: [
    { age: { $lt: 25 } },
    { city: "Chicago" }
  ]
})
```

#### Example Document Match:
```json
{
  "name": "Bob",
  "age": 22,
  "city": "San Francisco"
}
```
OR
```json
{
  "name": "Charlie",
  "age": 35,
  "city": "Chicago"
}
```

---

### **3. `$not` – Logical NOT**

#### Syntax:
```javascript
db.collection.find({
  <field>: { $not: { <condition> } }
})
```

#### Example:
Find documents where:
- Age **is NOT greater than 25**.

```javascript
db.collection.find({
  age: { $not: { $gt: 25 } }
})
```


### **Conclusion**

A database is essential for storing and managing data in any application. MongoDB is a powerful, flexible, and modern NoSQL database that allows developers to work with data in a way that matches their application’s needs. It’s especially suitable for applications that require speed, scalability, and flexibility.

## Additional Resources

- [MongoDB Documentation](https://www.mongodb.com/docs/)
- [MongoDB Tutorials](https://www.mongodb.com/learn)

