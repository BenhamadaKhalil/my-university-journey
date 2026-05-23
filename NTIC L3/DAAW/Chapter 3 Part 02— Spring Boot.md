# 🧠 **Chapter 3 Part 02— Spring Boot**

## **Part 02: The Model Layer & Repository**

---

## 🎯 **What Is the Model Layer?**

In **Spring Boot (MVC)**, the **Model Layer** is responsible for:

- 📦 **Data representation**
    
- 🗄 **Data access**
    
- ⚙ **Business logic**
    

### The Model Layer includes:

- **Entities**
    
- **Repositories (DAOs)**
    
- **Business Logic Layer**
    

📌 **Key idea**:

> The Model Layer = **what the application knows + how it stores data**

---

## 🧩 **Entities (Domain Objects)**

An **Entity**:

- Represents a **table** in the database
    
- Represents a **real-world object**
    
- Is a **Java class mapped to a database table**
    

### Important JPA Annotations:

- `@Entity` → marks the class as a database table
    
- `@Id` → primary key
    
- `@GeneratedValue` → auto-generates the ID
    

### Example (User Entity):

```java
@Entity
public class User {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;
  private String name;
  private String email;
}
```

🧠 **Memory trick**:

> Entity = **Java object ↔ Database row**

---

## 🔑 **Primary Key Generation Strategies**

`@GeneratedValue` strategies:

- `AUTO` → provider chooses
    
- `IDENTITY` → auto-increment (most common)
    
- `SEQUENCE` → database sequence
    
- `TABLE` → separate table
    

📌 With `IDENTITY`, the database generates the ID automatically when saving.

---

## 🗄 **Repository vs DAO (Very Important)**

### DAO (Old way)

- Manual SQL / HQL
    
- Lots of boilerplate
    
- Harder to test
    
- Weak Spring integration
    

### Repository (Modern Spring way)

- Built on **Spring Data JPA**
    
- Minimal code
    
- Auto-generated queries
    
- Full Spring integration
    

📌 **Conclusion**:

> In Spring Boot, **Repositories replace DAOs**

---

## 🧠 **What Is a Repository?**

A **Repository**:

- Acts as the **Data Access Layer (DAL)**
    
- Connects **Entities ↔ Database**
    
- Hides SQL and persistence details
    

### Main role:

- Save
    
- Read
    
- Update
    
- Delete data
    

📌 Repositories let you work with **objects**, not SQL.

---

## ⭐ **Why Repositories Are Powerful**

### 1️⃣ Separation of Concerns

- Business logic ≠ Data access
    
- Clean architecture
    

### 2️⃣ Data Source Abstraction

- Change DB without changing business logic
    
- SQL is hidden
    

### 3️⃣ Built-in CRUD (Spring Data JPA)

- `save()`
    
- `findById()`
    
- `findAll()`
    
- `deleteById()`
    

### 4️⃣ Transaction Management

- Ensures **data consistency**
    
- Automatic rollback on failure
    

### 5️⃣ Testability & Scalability

- Easy to mock
    
- Easy to scale
    

---

## 🔗 **JpaRepository in MVC Architecture**

### Model Layer

- Entities mapped to tables
    
- Repository handles persistence
    

### Service Layer

- Uses Repository
    
- Contains **business logic**
    
- No SQL here
    

### Controller Layer

- Uses Service only
    
- Never accesses database directly
    

📌 **Golden rule**:

> Controller → Service → Repository → Database

---

## 🧾 **Creating a Repository**

```java
public interface UserRepository
       extends JpaRepository<User, Long> {
}
```

✔ No implementation needed  
✔ Spring creates it automatically  
✔ Ready to inject

---

## 🔧 **Common JpaRepository Methods**

|Method|Purpose|
|---|---|
|`save()`|Insert / Update|
|`findById()`|Find by ID|
|`findAll()`|Retrieve all|
|`deleteById()`|Delete|
|`count()`|Count rows|
|`existsBy…()`|Check existence|

📌 **No boilerplate code needed**

---

## 📄 **Using Repository in Service Layer**

```java
@Service
public class UserService {
  private final UserRepository userRepository;

  public UserService(UserRepository userRepository) {
    this.userRepository = userRepository;
  }

  public User saveUser(User user) {
    return userRepository.save(user);
  }
}
```

🧠 **Service = brain, Repository = database bridge**

---

## 📊 **Pagination & Sorting**

- Sorting:
    

```java
userRepository.findAll(Sort.by("name").ascending());
```

- Pagination:
    

```java
PageRequest.of(0, 10);
```

📌 Used for **performance & scalability**

---

## 🔍 **Custom Query Methods (Magic of Spring Data)**

Spring creates queries from method names:

- `findByEmail(String email)`
    
- `countByStatus(String status)`
    
- `existsByEmail(String email)`
    
- `deleteByStatus(String status)`
    
- `findTop3ByOrderByScoreDesc()`
    

🧠 **Memory trick**:

> Method name = SQL query 😄

---

## 🧠 **Custom Queries with @Query**

When naming isn’t enough:

```java
@Query("SELECT u FROM User u WHERE u.name = :name")
List<User> findByName(@Param("name") String name);
```

✔ JPQL or SQL  
✔ Full control

---

## ✅ **Key Benefits of JpaRepository**

- 🚫 No boilerplate code
    
- 📖 Clean & readable
    
- 🔄 Flexible queries
    
- 🔐 Transaction safety
    
- 🏗 Follows best architecture practices
    

---

## 🧠 **Final Mental Model (EXAM GOLD)**

|Layer|Role|
|---|---|
|Entity|Database table|
|Repository|Data access|
|Service|Business logic|
|Controller|Request handling|

---

## 🧾 **Exam-Perfect Summary**

> The Model Layer in Spring Boot contains entities, repositories, and business logic. Repositories (via JpaRepository) abstract database access, provide built-in CRUD operations, support transactions, and integrate seamlessly with Spring MVC, resulting in clean, maintainable, and scalable applications.

---

If you want next, I can:

- 🔖 Turn this into **Obsidian flashcards**
    
- 📄 Create a **1-page Model Layer cheat sheet**
    
- ❓ Prepare **exam questions & answers**
    
- 🔄 Compare **JpaRepository vs CrudRepository**
    
- 🧪 Explain **@Transactional** deeply
    

Just tell me 👌

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DAAW/DAAW|◀ DAAW]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
