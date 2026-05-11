# 🔐🌿 **Chapter 7 — Spring Boot + Thymeleaf**

## **Security Login & CRUD Application**

---

## 🎯 **Chapter Goal**

- Build a **secure Spring Boot web application**
    
- Use:
    
    - **Spring Security**
        
    - **Thymeleaf**
        
    - **Role-based access**
        
    - **CRUD operations**
        
- Apply **real security best practices**
    

📌 **Key idea**:

> Security is part of the **architecture**, not an add-on.

---

## 🌐 **Why Thymeleaf?**

- Server-side **template engine**
    
- Integrates naturally with **Spring MVC**
    
- Generates **dynamic HTML**
    
- Secure by default (prevents XSS)
    

---

# 🛡 **Building a Secure Spring Boot Application**

---

## 1️⃣ **Implement HTTPS (Mandatory)**

- Encrypts data **in transit**
    
- Protects:
    
    - Credentials
        
    - Personal data
        
- HTTPS is **non-negotiable**
    

### Configuration example:

```properties
server.port=8443
server.ssl.key-store=classpath:keystore.jks
server.ssl.key-store-password=yourpassword
server.ssl.key-password=yourpassword
```

---

## 🔁 **Force HTTPS with Spring Security**

- Redirects all HTTP → HTTPS
    
- Works behind proxies (X-Forwarded-Proto)
    

📌 **Memory rule**:

> No HTTPS = No security

---

## 2️⃣ **Activate CSRF Protection**

- CSRF attacks trick users into unwanted actions
    
- Spring Security enables CSRF **by default**
    

🚫 **Never disable in production**

```java
http.csrf().disable(); // ❌ avoid
```

---

## 3️⃣ **Validate Input Rigorously**

- Never trust user input
    
- Validate:
    
    - Type
        
    - Length
        
    - Format
        
    - Range
        

Use Spring Validation:

```java
@NotEmpty(message = "Name cannot be empty")
private String name;
```

📌 **Golden rule**:

> All input is hostile until proven safe

---

## 4️⃣ **Use Parameterized Queries**

- Prevents **SQL Injection**
    
- Use:
    
    - JPA
        
    - Spring Data repositories
        

```java
@Query("SELECT u FROM User u WHERE u.email = :email")
User findByEmail(@Param("email") String email);
```

---

## 5️⃣ **Enable Method-Level Security**

- Prevent unauthorized access to sensitive methods
    
- Protect admin-only actions
    

```java
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser(Long id) { }
```

📌 **Defense in depth**

---

## 6️⃣ **Encrypt Sensitive Data**

- Protect:
    
    - Passwords
        
    - Secrets
        
- Encrypt configuration files
    

```java
@EncryptablePropertySource(
 name = "EncryptedProperties",
 value = "classpath:encrypted.properties"
)
```

---

## 7️⃣ **Proper Authentication & Authorization**

- Configure:
    
    - Authentication providers
        
    - `UserDetailsService`
        
    - Password encoders
        

📌 **Authentication** = who you are  
📌 **Authorization** = what you can do

---

# 👥 **Role-Based Access Control (RBAC)**

---

## 🔓 **Public Pages (All Users)**

- Home
    
- About Us
    
- Login
    

✔ Accessible without authentication

---

## 👑 **Admin Role**

- Access:
    
    - All pages
        
    - Admin dashboard
        
- Can manage:
    
    - Students
        
    - Teachers
        
    - Messages
        
- Full CRUD access
    

📌 Admin = full control

---

## 🎓 **Teacher Role**

- Access:
    
    - Add Courses
        
    - Upload files
        
    - Contact Us
        

📌 Teacher = content creator

---

## 📘 **Student Role**

- Access:
    
    - Contact Us
        
    - Public pages only
        

📌 Student = limited access

---

## 🚫 **Unauthorized Access**

- Accessing forbidden pages → **403 error**
    
- Spring Security blocks access automatically
    

📌 **Fail-safe default**

---

# 🧠 **Final Architecture View**

```
Browser
 ↓
Thymeleaf Views
 ↓
Controller
 ↓
Service
 ↓
Repository
 ↓
Database
```

🔐 Security filters intercept requests **before controllers**

---

## 🧠 **Final Mental Model (EXAM GOLD)**

| Concept         | Meaning                 |
| --------------- | ----------------------- |
| HTTPS           | Secure communication    |
| CSRF            | Fake request protection |
| Validation      | Input safety            |
| RBAC            | Role-based access       |
| Thymeleaf       | Secure HTML             |
| Spring Security | Access control          |

---

## 🧾 **Exam-Perfect Summary**

> A secure Spring Boot Thymeleaf application integrates HTTPS, CSRF protection, input validation, parameterized queries, method-level security, and role-based access control using Spring Security to provide authenticated login and secure CRUD operations.

---

If you want next, I can:

- 🔖 Convert this into **Obsidian flashcards**
    
- 📄 Make a **1-page security + CRUD cheat sheet**
    
- ❓ Generate **exam questions & answers**
    
- 🧪 Walk you through **a full project structure**
    
- 🔐 Compare **Thymeleaf security vs REST security**
    

Just tell me 👌