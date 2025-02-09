# MongoDB Setup and Usage Guide

## 📌 Prerequisites
Ensure you have the following installed on your system:
- [MongoDB](https://www.mongodb.com/try/download/community) (if using local database)
- [MongoDB Compass](https://www.mongodb.com/products/compass) (for GUI management)

## 🚀 Setting Up MongoDB Compass
1. **Download & Install MongoDB Compass:**
   - Go to [MongoDB Compass](https://www.mongodb.com/products/compass) and download the latest version.
   - Install it by following the setup instructions for your OS.

2. **Connect to MongoDB Server:**
   - Open MongoDB Compass.
   - In the "New Connection" window, enter your connection string:
     - For a local database: `mongodb://localhost:27017`
     - For a cloud database (MongoDB Atlas): use your connection string from Atlas.
   - Click **"Connect"** to establish the connection.

## 📂 Creating a Database and Collection
1. **Create a New Database:**
   - Click **"Create Database"** in MongoDB Compass.
   - Enter a database name (e.g., `Library`).
   - Enter a collection name (e.g., `books`).
   - Click **"Create Database"**.

2. **Insert Data into Collection:**
   - Navigate to the `Library` database → `books` collection.
   - Click **"Insert Document"**.
   - Add the following JSON data:
     ```json
     {
       "title": "Atomic Habits",
       "author": "James Clear",
       "publishedYear": 2018
     }
     ```
   - Click **"Insert"** to save the document.

## 🔍 Querying Data
- To retrieve all documents in the `books` collection:
  - Go to `Library` → `books`.
  - In the **Filter** bar, enter `{}`.
  - Click **Find**.
- To filter by author:
  - Enter `{ "author": "James Clear" }` in the **Filter** bar.
  - Click **Find**.

## ✏️ Updating Data
- Locate the document you want to edit.
- Click **"Edit Document"**, modify the fields, and **Save**.

## 🗑️ Deleting Data
- Find the document you want to delete.
- Click the **trash bin icon (🗑️)** next to the document.
- Confirm the deletion.

## 📊 Aggregation (Data Processing)
- Navigate to the **Aggregation** tab.
- Click **"Add Stage"** and select `$group`.
- Example: To calculate the average published year:
  ```json
  {
    "_id": null,
    "averageYear": { "$avg": "$publishedYear" }
  }
  ```
- Click **Run** to execute the aggregation.

## 📌 Indexing for Performance Optimization
1. Go to the **Indexes** tab.
2. Click **"Create Index"**.
3. Choose the field to index (e.g., `author: 1`).
4. Click **Create Index** to optimize search performance.

## 🔌 Connecting to MongoDB from a Node.js Application
If you want to interact with MongoDB from a **Node.js** app:
1. Install MongoDB driver:
   ```sh
   npm install mongodb
   ```
2. Connect to MongoDB in your script:
   ```javascript
   const { MongoClient } = require('mongodb');
   const uri = "mongodb://localhost:27017"; // Change for MongoDB Atlas if needed
   const client = new MongoClient(uri);

   async function run() {
       try {
           await client.connect();
           const db = client.db("Library");
           const books = db.collection("books");
           const results = await books.find({}).toArray();
           console.log(results);
       } finally {
           await client.close();
       }
   }
   run().catch(console.dir);
   ```

## 🎯 Conclusion
You now have a working MongoDB setup using **MongoDB Compass**! 🚀
- Use Compass for easy **CRUD operations**.
- Utilize **filtering, aggregation, and indexing** for data management.
- Connect MongoDB to your applications for advanced use cases.



