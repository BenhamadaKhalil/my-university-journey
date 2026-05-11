# 🧠 **Chapter 4 — Service & Controller Layers (Spring Boot)**
## 🎯 **Big Picture (Where These Layers Fit)**

```
Client
 ↓
Controller  →  Service  →  Repository  →  Database
```

📌 **Golden rule**:

> Controllers handle **HTTP**, Services handle **business logic**, Repositories handle **data**

---

# ⚙️ **THE SERVICE LAYER**

---

## 🧩 **What Is the Service Layer?**

The **Service Layer**:

- Contains **business logic**
    
- Acts as a **bridge** between Controller and Repository
    
- Ensures rules are applied **consistently**
    

📌 It answers the question:

> _“What should happen?”_

---

## 🎯 **Main Roles of the Service Layer**

### 1️⃣ Business Logic Management

- Centralizes all **business rules**
    
- Prevents logic duplication
    
- Keeps controllers clean
    

---

### 2️⃣ Interaction with Repository

- Calls repository methods
    
- Performs CRUD operations
    
- Controllers never access repositories directly
    

---

### 3️⃣ Transaction Management

- Uses `@Transactional`
    
- Ensures:
    
    - All operations succeed ✅
        
    - Or everything rolls back ❌
        

📌 **Atomicity** = all or nothing

---

### 4️⃣ Validation & Error Handling

- Validates input data
    
- Applies business constraints
    
- Handles exceptions gracefully
    

---

### 5️⃣ Separation of Concerns

- Controller ≠ Business logic
    
- Service ≠ HTTP handling
    

✔ Cleaner  
✔ Testable  
✔ Maintainable

---

### 6️⃣ Reusability

- Same service can be used by:
    
    - Multiple controllers
        
    - Multiple applications
        

---

### 7️⃣ Integration with Other Services

- Can call:
    
    - Other microservices
        
    - External APIs
        

---

## 🧱 **Service Classes in Spring Boot**

A service class:

- Is a **Java class**
    
- Annotated with `@Service`
    
- Uses **constructor injection**
    
- Calls repositories
    

---

### 🛠 **Service Interface Example**

```java
public interface UserService {
  User createUser(User user);
  Optional<User> getUserById(Long id);
  List<User> getAllUsers();
  User updateUser(Long id, User user);
  void deleteUser(Long id);
}
```

---

### 🧠 **Service Implementation Example**

```java
@Service
public class UserServiceImpl implements UserService {

  private final UserRepository userRepository;

  public UserServiceImpl(UserRepository userRepository) {
    this.userRepository = userRepository;
  }

  public User createUser(User user) {
    return userRepository.save(user);
  }
}
```

📌 **Best practice**:

> Interface + Implementation

---

# 🌐 **THE CONTROLLER LAYER**

---

## 🧩 **What Is the Controller Layer?**

The **Controller Layer**:

- Handles **HTTP requests**
    
- Routes requests to the correct service
    
- Sends **HTTP responses**
    

📌 It answers the question:

> _“How does the client interact with the system?”_

---

## 🎯 **Controller Responsibilities**

- 📍 Routing (URL → method)
    
- 📥 Request handling (JSON, params)
    
- 📤 Response management (JSON, status codes)
    

---

## 🧱 **Structure of a Controller**

Controllers are:

- Annotated with `@RestController` or `@Controller`
    
- Use mapping annotations
    
- Inject services
    

---

### 🛠 **Controller Example**

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

  private final UserService userService;

  public UserController(UserService userService) {
    this.userService = userService;
  }
}
```

---

## 🔑 **Key Controller Annotations (EXAM GOLD)**

| Annotation        | Role                   |
| ----------------- | ---------------------- |
| `@RestController` | REST controller (JSON) |
| `@Controller`     | MVC controller (views) |
| `@RequestMapping` | Base URL               |
| `@GetMapping`     | Read                   |
| `@PostMapping`    | Create                 |
| `@PutMapping`     | Update                 |
| `@DeleteMapping`  | Delete                 |
| `@PathVariable`   | URL variable           |
| `@RequestParam`   | Query parameter        |
| `@RequestBody`    | JSON → Object          |

| Feature      | `@RequestBody`   | `@RequestParam` |
| ------------ | ---------------- | --------------- |
| Data source  | Request body     | URL parameters  |
| HTTP methods | POST, PUT, PATCH | GET, POST       |
| Data size    | Large            | Small           |
| Content type | JSON / XML       | Query/Form      |

/users/5        → @PathVariable
/users?id=5     → @RequestParam
POST /users     → @RequestBody

---

## 🔁 **CRUD Operations in Controller**

### ➕ Create

```java
@PostMapping
public ResponseEntity<User> createUser(@RequestBody User user) {
  return new ResponseEntity<>(userService.createUser(user),
                              HttpStatus.CREATED);
}
```

---

### 📖 Read

```java
@GetMapping("/{id}")
public ResponseEntity<User> getUser(@PathVariable Long id) {
  return userService.getUserById(id)
    .map(ResponseEntity::ok)
    .orElse(ResponseEntity.notFound().build());
}
```

---

### ✏ Update

```java
@PutMapping("/{id}")
public ResponseEntity<User> updateUser(@PathVariable Long id,
                                       @RequestBody User user) {
  return ResponseEntity.ok(userService.updateUser(id, user));
}
```

---

### ❌ Delete

```java
@DeleteMapping("/{id}")
public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
  userService.deleteUser(id);
  return ResponseEntity.noContent().build();
}
```

---

## ✅ **Validation & Error Handling**

- Use `@Valid` for input validation
    
- Handles invalid data automatically
    

```java
@PostMapping
public ResponseEntity<User> createUser(@Valid @RequestBody User user) {
  return new ResponseEntity<>(userService.createUser(user),
                              HttpStatus.CREATED);
}
```

---

## 🧠 **Key Architectural Rules (VERY IMPORTANT)**

🚫 Controller should NOT:

- Contain business logic
    
- Access repositories directly
    

🚫 Service should NOT:

- Handle HTTP
    
- Return ResponseEntity
    

---

## 🧠 **Final Mental Model (EXAM READY)**

|Layer|Responsibility|
|---|---|
|Controller|HTTP & Routing|
|Service|Business Logic|
|Repository|Data Access|
|Entity|Database Mapping|

---

## 🧾 **Exam-Perfect Summary**

> The Service layer contains the business logic and manages transactions, acting as an intermediary between controllers and repositories. The Controller layer handles HTTP requests, routes them to services, and returns appropriate responses, ensuring a clean separation of concerns in Spring Boot applications.

---

If you want next, I can:

- 🔖 Turn this into **Obsidian flashcards**
    
- 📄 Create a **1-page MVC + Spring Boot cheat sheet**
    
- ❓ Generate **exam questions & answers**
    
- 🔄 Explain **@Transactional deeply**
    
- 🧪 Show a **full CRUD project structure**
    

Just tell me 👌