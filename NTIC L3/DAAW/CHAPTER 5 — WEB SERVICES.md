# 🌐 CHAPTER V — WEB SERVICES (REST API)

## 🎯 What is a Web Service?

A **Web Service** is a standardized way for **applications to communicate over the internet**, regardless of:

- Programming language
    
- Platform
    
- Technology
    

➡ Uses **open standards & protocols** (mainly HTTP).  
➡ Enables **interoperability**.

---

## 🔹 Types of Web Services

### 1️⃣ SOAP (Simple Object Access Protocol)

- **Protocol** (strict rules)
    
- Uses **XML**
    
- Strong security & contracts (**WSDL**)
    
- Built-in error handling
    
- Heavy & complex
    

📌 **Used for**: Enterprise systems, banking, ACID compliance.

---

### 2️⃣ REST (Representational State Transfer)

- **Architectural style** (❗ not a protocol)
    
- Uses **HTTP methods**
    
- Data formats: **JSON (mostly)**, XML
    
- Lightweight & scalable
    

📌 **Used for**: Web apps, mobile apps, microservices

---

## 🔹 REST Basics (VERY IMPORTANT)

- Introduced by **Roy Fielding (2000)**
    
- REST = **REpresentational State Transfer**
    
- A service is **RESTful** only if it respects REST constraints
    

---

## 🧱 REST Architecture: Client–Server

- **Client** → sends HTTP request
    
- **Server** → returns response (JSON/XML)
    
- Clear separation:
    
    - Client → UI
        
    - Server → data & logic
        

✔ Easier maintenance  
✔ Independent evolution

---

## 🔑 REST CONSTRAINTS (EXAM FAVORITES)

### 1️⃣ Statelessness

- Each request contains **all needed information**
    
- Server stores **no client session**
    

✅ Easier scaling  
✅ Less server memory

---

### 2️⃣ Client–Server

- UI ≠ Data logic
    
- Multiple clients (web, mobile…)
    

---

### 3️⃣ Uniform Interface

Achieved by:

- Resources identified by **URI**
    
- Manipulation via **representations (JSON/XML)**
    
- **Self-descriptive messages**
    
- **HATEOAS** (links guide the client)
    

---

### 4️⃣ Resource-Based

Everything is a **resource** identified by a URI.

```
/users
/users/{id}
```

---

### 5️⃣ Layered System

- Client doesn’t know internal layers
    
- Example: Load balancer → server
    

✅ Security  
✅ Scalability

---

### 6️⃣ Cacheable

- Responses specify if cacheable
    
- Improves performance
    

---

## 🔄 CRUD ↔ HTTP METHODS (⚠️ MUST MEMORIZE)

|CRUD|HTTP|
|---|---|
|Create|POST|
|Read|GET|
|Update|PUT|
|Delete|DELETE|

---

## 🧩 Designing a REST API (Spring Boot Logic)

### 1️⃣ Define API Purpose

- Understand business logic
    
- Identify **resources**
    
- Define supported **operations (CRUD)**
    

---

### 2️⃣ URI Design (EndPoints)

✔ URIs = **nouns**, not verbs

✅ Correct:

```
GET /users
GET /users/{id}
POST /users
PUT /users/{id}
DELETE /users/{id}
```

❌ Wrong:

```
/getUsers
/deleteUser
```

---

### 3️⃣ API Versioning

Prevents breaking old clients.

```
/v1/users
/v2/users
```

---

## 📡 HTTP STATUS CODES (EXAM GOLD)

### ✅ 2xx — Success

- **200 OK** → GET success
    
- **201 Created** → POST success
    
- **204 No Content** → DELETE success
    

---

### ❌ 4xx — Client Errors

- **400** Bad Request
    
- **401** Unauthorized
    
- **403** Forbidden
    
- **404** Not Found
    

---

### 🔥 5xx — Server Errors

- **500** Internal Server Error
    
- **503** Service Unavailable
    

---

## 📦 Request & Response Payloads

### DTOs (Data Transfer Objects)

❗ Separate from database entities

- **Input DTO** → request
    
- **Output DTO** → response
    

---

### JSON Example

**Request**

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securePassword"
}
```

**Response**

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com"
}
```

---

## ⚠️ Error Handling (Spring Boot)

- Centralized using `@ControllerAdvice`
    
- Always return **clear messages + status**
    

```json
{
  "status": 404,
  "error": "Not Found",
  "message": "User with ID 123 not found"
}
```

---

## 🧠 EXAM KEYWORDS TO REMEMBER

- REST ≠ protocol
    
- Stateless
    
- Resource-based
    
- URI = noun
    
- CRUD ↔ HTTP methods
    
- JSON
    
- DTO
    
- HTTP status codes
    
- @ControllerAdvice
    

---

If you want, next I can:

- 🔥 Create **QCM questions**
    
- 🧪 Give **Spring Boot code examples**
    
- 📝 Make a **1-page ultra-cheat-sheet**
    
- 🧠 Add **mnemonics for memorization**
    

Just tell me 👍

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DAAW/DAAW|◀ DAAW]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
