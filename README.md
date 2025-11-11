# 🧩 Node.js Lab – Error Handling in Express

## 📘 Overview
In this lab, you will build a simple **Product Management API** using **Node.js and Express** that demonstrates proper **error handling practices** in backend development.

The objective is to help you understand how to:
- Handle different types of runtime and operational errors in Express.
- Structure error-handling middleware.
- Validate and manage request data properly.
- Work with asynchronous file operations using the Node.js `fs/promises` module.

<!-- ## 🎯 Learning Objectives
By the end of this lab, you will be able to:
1. Create and use Express routes and controllers.
2. Handle errors using **custom middleware** and the built-in Express error flow.
3. Manage async errors from file operations (read/write).
4. Validate request data and return appropriate HTTP status codes.
5. Write clean and modular Node.js code. -->

---

## 🧠 Problem Statement

You are building a **Product Management REST API** that allows users to:
- View all products  
- View a specific product by ID  
- Add a new product  

The product data will be stored locally in a `products.json` file inside the `data` folder.

Your main focus is to **implement proper error handling** across the application.

---

## 🏗️ Project Structure

Your project should have the following folder layout:

```
Error-Handling/
│
├── controllers/
│   └── productController.js
├── data/ 
│   └── products.json          
├── middleware/            
│   └── errorHandler.js               
├── routes/
│   └── productRoutes.js                
├── src/
│   └── server.js                  
├── test/               
│   └── product.test.js
└── README.md                   
```

---

## 🧩 Tasks to Complete

### **1️⃣ Global Error Handling Middleware**

Create a centralized error-handling middleware inside  
`/middleware/errorHandler.js` that catches all errors in one place.

Example:
```js
app.use((err, req, res, next) => {
  // Logic to handle errors globally
});
```

Error should be sent in JSON format like :
```json
{  "error": "Internal Server Error" }
```

---

### **2️⃣ Route for Undefined Endpoints (404 Handler)**

In your `app.js`, define a route handler for any undefined routes. 

Example:
```js
app.use((req, res) => {
  // Logic to handle undefined routes
});
```

Error should be sent in JSON format like :
```json
{  "error": "Route not found" }
```

---

### **3️⃣ Controller: Get All Products**

Inside `controllers/productController.js`, implement:

Example:
```js
export const getAllProducts = async (req, res, next) => {
  try {
    // Read from products.json using fs/promises
    // Send the list of products as JSON
  } catch (err) {
    next(err); // Pass error to middleware
  }
};
```

Should return a list of all products in JSON format.
```json
{  "products": products }
```

---

### **4️⃣ Controller: Get Product by ID**

Implement:

Example:
```js
export const getProductById = async (req, res, next) => {
    // Extract id from params
    // Find product by id
    // If not found, return 404 with { error: "Product not found" }
};
```

- If product not found → respond with :
```json
{  "error": "Product not found" }
```
and `404 Not Found` status code.

- On success → return:
```json
{ "id": 1, "name": "Product Name", "price": 100 }
```

---

### **5️⃣ Controller: Add Product**

Implement:

Example:
```js
export const addProduct = async (req, res, next) => {
  try {
    // Validate name and price fields
    // Read existing products from file
    // Create new product object with auto-incremented ID
    // Write back to products.json
    // Return 201 Created with the new product
  } catch (err) {
    next(err);
  }
};
```

- If validation fails → respond with :
```json
{ "error": "Invalid product data" }
```
and `400 Bad Request` status code.

- On success → return:
```json
{ "id": 1, "name": "Product Name", "price": 100 }
```

## **⚡ Error Types to Handle** {#error-types-to-handle}

Your application should gracefully handle the following:

| **Type**              | **Example**                        | **Response**                                   |
|-----------------------|------------------------------------|------------------------------------------------|
| **Validation Error**  | Missing name or invalid price      | { \"error\": \"Invalid product data\" } (400)  |
| **Not Found Error**   | Product ID doesn't exist           | { \"error\": \"Product not found\" } (404)     |
| **File System Error** | products.json is missing/corrupted | { \"error\": \"Internal Server Error\" } (500) |
| **Undefined Route**   | /random endpoint                   | { \"error\": \"Route not found\" } (404)       |

---

## **Installing and Running Your Application**
Run the following command to install all required dependencies:

```bash
npm install
```

Run the following command to start the server:

```bash
npm run dev
```


## **🧪 Testing Your Implementation** {#testing-your-implementation}

A complete `product.test.js` file is provided inside /test.

Run tests with:

```bash
npm test
```

You should see test cases covering:

- ✅ Successful CRUD operations (Create, Read, Update, Delete)

- ❌ Error handling (Invalid data, Not Found, Corrupted File)

Keep running tests until all pass successfully!!
