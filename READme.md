
### **Array Operators with Syntax and Examples**  

#### **1. `$in` Operator (Matches any value in an array)**  
**Syntax:**  
```json
{ field: { $in: [value1, value2, ...] } }
```  
**Example:**  
Find users who live in either "New York" or "Chicago".  
```json
db.users.find({ city: { $in: ["New York", "Chicago"] } })
```  

#### **2. `$nin` Operator (Matches none of the values in an array)**  
**Syntax:**  
```json
{ field: { $nin: [value1, value2, ...] } }
```  
**Example:**  
Find users who do **not** live in "New York" or "Chicago".  
```json
db.users.find({ city: { $nin: ["New York", "Chicago"] } })
```  


### **What is Aggregation in MongoDB?**  
Aggregation in MongoDB is a **data processing framework** used to perform complex transformations and computations on collections of documents. It works like a **pipeline**, where documents go through multiple stages, such as filtering, grouping, sorting, and calculating aggregate values.  

### **How Aggregation Works?**  
MongoDB’s aggregation framework processes data through a **pipeline of stages**, each transforming the documents before passing them to the next stage.  

#### **Example Aggregation Pipeline:**  
```json
db.orders.aggregate([
  { $match: { status: "Completed" } },  // Stage 1: Filter completed orders
  { $group: { _id: "$customerId", totalAmount: { $sum: "$amount" } } },  // Stage 2: Group by customer and sum amounts
  { $sort: { totalAmount: -1 } }  // Stage 3: Sort by total amount (descending)
])
```
### **Key Aggregation Stages:**  

1. **`$match`** → Filters documents based on a condition (like `WHERE` in SQL).  
   ```json
   { $match: { status: "Completed" } }
   ```  
2. **`$group`** → Groups documents and applies aggregate functions (`$sum`, `$avg`, `$max`, etc.).  
   ```json
   { $group: { _id: "$customerId", totalSpent: { $sum: "$amount" } } }
   ```  
3. **`$sort`** → Sorts results in ascending (1) or descending (-1) order.  
   ```json
   { $sort: { totalSpent: -1 } }
   ```  
4. **`$project`** → Selects specific fields to return.  
   ```json
   { $project: { name: 1, totalSpent: 1 } }
   ```  
5. **`$limit` & `$skip`** → Controls the number of documents in the output (like `LIMIT` and `OFFSET` in SQL).  
   ```json
   { $limit: 10 }
   ```  
6. **`$lookup`** → Performs a **join** with another collection.  
   ```json
   { $lookup: { from: "customers", localField: "customerId", foreignField: "_id", as: "customerDetails" } }
   ```  

### **Why Use Aggregation?**  
✅ Faster than multiple queries  
✅ Reduces data processing in applications  
✅ Works efficiently on large datasets  

### **Real-Time Examples of MongoDB Aggregation**  

#### ** E-Commerce: Total Sales per Product**  
 *Find the total sales for each product in an online store.*  
 **Collection Name:** `orders`  
```json
[
  { "_id": 1, "productId": "P1001", "amount": 200, "status": "Completed" },
  { "_id": 2, "productId": "P1002", "amount": 350, "status": "Completed" },
  { "_id": 3, "productId": "P1001", "amount": 150, "status": "Pending" },
  { "_id": 4, "productId": "P1003", "amount": 500, "status": "Completed" },
  { "_id": 5, "productId": "P1002", "amount": 400, "status": "Completed" }
]
```
**Query:**  
```json
db.orders.aggregate([
  { $match: { status: "Completed" } },  // Filter only completed orders
  { $group: { _id: "$productId", totalSales: { $sum: "$amount" } } },  // Sum sales per product
  { $sort: { totalSales: -1 } }  // Sort by highest sales
])
```


---

#### ** Social Media: Count Posts per User**  
 **Collection Name:** `posts`  
```json
[
  { "_id": 1, "userId": "U001", "content": "Hello World!" },
  { "_id": 2, "userId": "U002", "content": "MongoDB is awesome!" },
  { "_id": 3, "userId": "U001", "content": "Aggregation framework rocks!" },
  { "_id": 4, "userId": "U003", "content": "Let's learn MongoDB" },
  { "_id": 5, "userId": "U001", "content": "Another post from me" }
]
```
*Find the number of posts each user has made.*  

**Query:**  
```json
db.posts.aggregate([
  { $group: { _id: "$userId", postCount: { $sum: 1 } } },  // Count posts per user
  { $sort: { postCount: -1 } }  // Sort by most active users
])
```
**Use Case:** Helps identify the most active users.  

---



#### ** Ride-Sharing App: Total Earnings per Driver**  
 *Calculate total earnings for each driver.*  
 **Collection Name:** `rides`  
```json
[
  { "_id": 1, "driverId": "D100", "fare": 50, "status": "Completed" },
  { "_id": 2, "driverId": "D101", "fare": 80, "status": "Completed" },
  { "_id": 3, "driverId": "D100", "fare": 100, "status": "Completed" },
  { "_id": 4, "driverId": "D102", "fare": 60, "status": "Completed" },
  { "_id": 5, "driverId": "D101", "fare": 90, "status": "Completed" }
]
```
**Query:**  
```json
db.rides.aggregate([
  { $match: { status: "Completed" } },  // Only completed rides
  { $group: { _id: "$driverId", totalEarnings: { $sum: "$fare" } } },
  { $sort: { totalEarnings: -1 } }
])
```


 
