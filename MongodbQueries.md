# MongoDB Assignment Documentation

## 1. Database Collection Creation

### Creating the `Library` Database
```javascript
use Library;
```

### Inserting Books into the `books` Collection
```javascript
db.books.insertMany([
   {
      "title": "The Great Gatsby",
      "author": "F. Scott Fitzgerald",
      "publishedYear": 1925,
      "genre": "Classic",
      "ISBN": "978-0-06-112008-4"
   },
   {
      "title": "Java Programming",
      "author": "Emilly Morrison",
      "publishedYear": 2018,
      "genre": "Programming",
      "ISBN": "978-0-06-113002-1"
   },
   {
      "title": "The Psychology of Money",
      "author": "Morgan Housel",
      "publishedYear": 2020,
      "genre": "Finance",
      "ISBN": "978-0-452-28423-4"
   },
   {
      "title": "Atomic Habits",
      "author": "James Clear",
      "publishedYear": 2018,
      "genre": "Self Improvement",
      "ISBN": "978-0-7432-7356-5"
   },
   {
      "title": "The Conspirator's Hierarchy",
      "author": "Dr. John Coleman",
      "publishedYear": 1990,
      "genre": "Adventure",
      "ISBN": "978-0-14-243724-7"
   }
]);
```

## 2. Retrieving Data

### Retrieve All Books
```javascript
db.getCollection('Books').find({});
```

### Retrieve Books by a Specific Author
```javascript
db.getCollection('Books').find({ author: 'James Clear' });
```

### Retrieve Books Published After 2000
```javascript
db.getCollection('Books').find({ publishedYear: { $gt: 2000 } });
```

## 3. Updating Data

### Update a Book's Published Year
```javascript
db.getCollection('Books').updateOne(
  { "title": "Java Programming" },
  { "$set": { "publishedYear": 2019 } }
);
```

### Add a Rating Field to a Book
```javascript
db.getCollection('Books').updateOne(
  { "title": "Java Programming" },
  { "$set": { "rating": 4.5 } }
);
```

## 4. Deleting Data

### Delete by ISBN
```javascript
db.getCollection('Books').deleteOne({ "ISBN": "978-0-06-112008-4" });
```

### Delete by Genre
```javascript
db.getCollection('Books').deleteMany({ "genre": "Programming" });
```

## 5. Data Modeling

### Users Collection
```javascript
{
  "name": "Alice Johnson",
  "email": "alice@example.com",
  "address": "123 Main St, NY",
  "phone": "+123456789",
  "createdAt": ISODate("2024-02-09T12:00:00.000Z")
}
```

### Products Collection
```javascript
{
  "name": "Laptop",
  "brand": "Dell",
  "price": 1200,
  "stock": 50,
  "category": "Electronics"
}
```

### Orders Collection
```javascript
{
  "userId": ObjectId("660d8f9b123456789abcdeff"),
  "products": [
    {
      "productId": ObjectId("660d8f9b123456789abcdf01"),
      "quantity": 2
    }
  ],
  "totalAmount": 2400,
  "orderDate": ISODate("2024-02-09T15:30:00.000Z")
}
```

## 6. Aggregation Pipeline

### Count Books by Genre
```javascript
db.books.aggregate([
  {
    "$group": {
      "_id": "$genre",
      "totalBooks": { "$sum": 1 }
    }
  }
]);
```

### Calculate Average Published Year
```javascript
db.books.aggregate([
  {
    "$group": {
      "_id": null,
      "averageYear": { "$avg": "$publishedYear" }
    }
  }
]);
```

### Find Top-Rated Book
```javascript
db.books.find().sort({ "rating": -1 }).limit(1);
```

## 7. Indexing in MongoDB

### Benefits of Indexing
- **Speeds up queries** (e.g., searching by author).
- **Optimizes filtering & sorting**.
- **Reduces performance issues** on large datasets.

### Creating an Index on Author Field
```javascript
db.books.createIndex({ "author": 1 });
```

