
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

Would you like a **real-world example** to practice? 😊