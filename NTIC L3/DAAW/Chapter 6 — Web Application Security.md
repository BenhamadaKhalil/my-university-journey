# 🔐 **Chapter 6 — Web Application Security**
## 🎯 **Why Security Matters**

- 🌐 75% of cyberattacks target **web applications**
    
- Security is a **non-functional requirement**
    
- Must be integrated into:
    
    - Design
        
    - Development
        
    - Deployment
        

📌 **Key idea**:

> Security is **not optional** and not an afterthought.

---

## 🛡 **Why Web Security Is Important**

- 🔒 **Protect user data**
    
    - Credentials
        
    - Financial data
        
    - Personal information
        
- 🤝 **Maintain user trust**
    
- 📜 **Legal compliance**
    
    - GDPR
        
    - PCI-DSS
        
- 💼 **Business continuity**
    
    - Prevent downtime
        
    - Protect reputation
        

---

## ⚠️ **Web Application Security Risks (OWASP)**

Common risks include:

- Broken Access Control
    
- Cryptographic Failures
    
- Injection (SQL, XSS)
    
- Insecure Design
    
- Security Misconfiguration
    
- Vulnerable Components
    
- Authentication Failures
    
- Logging & Monitoring Failures
    
- SSRF
    

📌 **Memory trick**:

> Most attacks exploit **bad input + weak access control**

---

## 🔑 **Key Areas of Web Security**

---

### 1️⃣ Authentication & Authorization

#### 🔐 Authentication

- Verifies **who the user is**
    
- Examples:
    
    - Username / Password
        
    - MFA
        
    - Biometrics
        

#### 🛂 Authorization

- Verifies **what the user can do**
    
- Examples:
    
    - Role-based access (ADMIN, USER)
        

📌 **Rule**:

> Authentication first → Authorization second

---

### 2️⃣ Encryption

- Use **HTTPS**
    
- Protects data in transit
    
- Prevents:
    
    - Eavesdropping
        
    - Tampering
        

---

### 3️⃣ Input Validation & Sanitization

- Prevents:
    
    - SQL Injection
        
    - XSS
        
- Validate:
    
    - Forms
        
    - URLs
        
    - JSON input
        

📌 **Golden rule**:

> Never trust user input ❌

---

### 4️⃣ Cross-Site Scripting (XSS)

- Injects malicious scripts
    
- Affects other users
    

🛡 Prevention:

- Input sanitization
    
- Content Security Policy (CSP)
    

---

### 5️⃣ Cross-Site Request Forgery (CSRF)

- Tricks users into unwanted actions
    

🛡 Prevention:

- CSRF tokens
    
- Request validation
    

---

### 6️⃣ Session Management

- Secure cookies
    
- Token-based authentication (JWT)
    
- Session timeouts
    

🛡 Goal:

> Prevent session hijacking

---

### 7️⃣ Secure Coding Practices

- Avoid:
    
    - Buffer overflows
        
    - Exposed APIs
        
    - Poor data handling
        

---

### 8️⃣ Firewalls & Security Headers

- Web Application Firewalls (WAF)
    
- Security headers:
    
    - HSTS
        
    - X-Frame-Options
        

---

### 9️⃣ Patching, Monitoring & Logging

- Regular updates
    
- Continuous monitoring
    
- Log security events
    

📌 **Detect early → respond faster**

---

# 🔐 **Security in Spring Boot**

---

## 🌱 **Spring Security**

- Default security framework for Spring
    
- Handles:
    
    - Authentication
        
    - Authorization
        
- Highly customizable
    
- Integrated via:
    
    - `spring-boot-starter-security`
        

📌 **Fact**:

> Spring Security = de-facto standard

---

## 🔄 **How Spring Security Works**

- Based on **JAAS**
    
- Uses **Filters**
    
- Applies security **before controller execution**
    

### Request Flow:

```
Request
 ↓
Security Filter (Authentication + Authorization)
 ↓
DispatcherServlet
 ↓
Controller
 ↓
Response
```

🧠 **Key component**:

- `DelegatingFilterProxy`
    

---

## 🔐 **Authentication in Spring Security**

- Verifies user identity
    
- Common method:
    
    - Username + Password
        
- Enables authorization after success
    
- Built-in authentication support
    

---

## 🛂 **Authorization in Spring Security**

- Defines **who can access what**
    
- Works at:
    
    - Request level
        
    - Method level
        

📌 Supports **defense in depth**:

> Multiple security layers protect the app

---

## 🧠 **Final Mental Model (EXAM READY)**

| Concept         | Meaning              |
| --------------- | -------------------- |
| Authentication  | Who you are          |
| Authorization   | What you can access  |
| HTTPS           | Secure communication |
| XSS             | Script injection     |
| CSRF            | Fake requests        |
| Spring Security | Protection framework |

---

## 🧾 **Exam-Perfect Summary**

> Web security is a fundamental requirement that protects user data, ensures trust, and maintains business continuity. Spring Security provides robust authentication and authorization mechanisms using filters, enabling secure access control and defense-in-depth for Spring Boot applications.

---

If you want next, I can:

- 🔖 Convert this into **Obsidian flashcards**
    
- 📄 Make a **1-page Security cheat sheet**
    
- ❓ Generate **exam Q&A**
    
- 🔐 Explain **JWT vs Session-based auth**
    
- 🧪 Show **Spring Security config examples**
    

Just tell me 👌

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DAAW/DAAW|◀ DAAW]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
