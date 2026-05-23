# ✅ TP MASTER LESSON — Spring Boot from 0 → MVC → CRUD → MySQL → Security

## 0) The Architecture you MUST draw in exam

```
Browser/Client
   ↓ HTTP
Controller  (routing + model)
   ↓ calls
Service     (business logic + transactions)
   ↓ calls
Repository  (data access)
   ↓
DB (MySQL)  OR in-memory List
```

This is exactly what your TPs build step-by-step.

---

## TP02 — Setup + Run + “Hello World”

### What they ask

- commands to verify Java/Maven
    
- run Spring Boot in VSCode
    
- a controller with `@GetMapping`
    

### Code template (fill-the-gap ready)

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

  @GetMapping("/hello")
  public String hello() {
    return "Hello, World!";
  }
}
```

This matches your TP exactly.

Run:

```bash
mvn spring-boot:run
```

---

## TP03 — MVC Basics (Controller → Model → Thymeleaf View)

### Goal

Hardcode a list of students in controller, pass it to view with `Model`.

### Must-memorize

- `@Controller` (MVC, returns view name)
    
- `Model model`
    
- `model.addAttribute("students", students)`
    
- Thymeleaf `th:each` + `th:text`
    

### Code template

**Student model**

```java
public class Student {
  private String name;
  private String email;
  private int age;

  // constructor + getters/setters
}
```

**Controller**

```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class StudentController {

  @GetMapping("/students")
  public String getStudents(Model model) {
    // create list hardcoded
    model.addAttribute("students", students);
    return "students"; // students.html
  }
}
```

**students.html**

```html
<html xmlns:th="http://www.thymeleaf.org">
<body>
<table>
  <tr th:each="student : ${students}">
    <td th:text="${student.name}"></td>
    <td th:text="${student.email}"></td>
    <td th:text="${student.age}"></td>
  </tr>
</table>
</body>
</html>
```

---

## TP04 — Add Service + Repository (in-memory List)

### Goal

Separate layers:

- repository = list storage
    
- service = business logic
    
- controller = request handling
    

### Key exam rule

> Controller should NOT manage the list directly → it calls Service → Service calls Repository.

### Code templates

**Repository**

```java
@Repository
public class StudentRepository {
  private List<Student> students = new ArrayList<>();

  public StudentRepository() {
    students.add(new Student("mohamed","med@example.com",25));
  }

  public List<Student> findAll() { return students; }
  public void addStudent(Student student) { students.add(student); }
}
```

**Service**

```java
@Service
public class StudentService {
  private final StudentRepository studentRepository;

  public StudentService(StudentRepository studentRepository){
    this.studentRepository = studentRepository;
  }

  public List<Student> getAllStudents() {
    return studentRepository.findAll();
  }

  public void addStudent(Student s){
    studentRepository.addStudent(s);
  }
}
```

**Controller POST add**

```java
@PostMapping("/students/add")
public String addStudent(@RequestParam String name,
                         @RequestParam String email,
                         @RequestParam int age) {
  Student student = new Student(name,email,age);
  studentService.addStudent(student);
  return "redirect:/students";
}
```

---

## TP05/06 — Connect to MySQL + Full CRUD + Thymeleaf forms

### Goal

Now your repository becomes a **JPA repository**, and students are stored in **MySQL**.

### Critical exam keys

- `application.properties` DB config
    
- Entity annotations `@Entity @Table @Id @GeneratedValue`
    
- `StudentRepository extends JpaRepository<Student, Long>`
    
- CRUD endpoints + Thymeleaf form binding: `th:object`, `th:field`
    

### application.properties (fill gaps)

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/student-db
spring.datasource.username=NAME
spring.datasource.password=PASS
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

### Entity

```java
@Entity
@Table(name="students")
public class Student {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;
  // name,email,age
}
```

### Repository

```java
public interface StudentRepository extends JpaRepository<Student, Long> {}
```

### Service CRUD

```java
@Service
public class StudentService {
  @Autowired private StudentRepository studentRepository;

  public List<Student> getAllStudents(){ return studentRepository.findAll(); }
  public void saveStudent(Student s){ studentRepository.save(s); }
  public Student getStudentById(Long id){ return studentRepository.findById(id).orElse(null); }
  public void deleteStudent(Long id){ studentRepository.deleteById(id); }
}
```

### Controller CRUD (most important)

```java
@Controller
@RequestMapping("/students")
public class StudentController {

  @Autowired private StudentService studentService;

  @GetMapping
  public String listStudents(Model model){
    model.addAttribute("students", studentService.getAllStudents());
    return "student-list";
  }

  @GetMapping("/add")
  public String showAddForm(Model model){
    model.addAttribute("student", new Student());
    return "student-form";
  }

  @PostMapping("/save")
  public String saveStudent(@ModelAttribute("student") Student student){
    studentService.saveStudent(student);
    return "redirect:/students";
  }

  @GetMapping("/edit/{id}")
  public String showEditForm(@PathVariable Long id, Model model){
    model.addAttribute("student", studentService.getStudentById(id));
    return "student-form";
  }

  @GetMapping("/delete/{id}")
  public String deleteStudent(@PathVariable Long id){
    studentService.deleteStudent(id);
    return "redirect:/students";
  }
}
```

### Thymeleaf form binding

```html
<form th:action="@{/students/save}" th:object="${student}" method="post">
  <input type="hidden" th:field="*{id}"/>
  <input type="text" th:field="*{name}" required/>
  <input type="text" th:field="*{email}" required/>
  <input type="number" th:field="*{age}" required/>
  <button type="submit">Submit</button>
</form>
```

---

## TP07 — Test with Postman (REST mindset)

### What they want

- Understand HTTP verbs:
    
    - GET retrieve
        
    - POST create
        
    - PUT update
        
    - DELETE delete
        

Example endpoints:

- `GET http://localhost:8080/api/students`
    
- `POST http://localhost:8080/api/students` with JSON body
    

📌 Exam trap:

> Postman tests REST endpoints (usually `@RestController`), not Thymeleaf views.

---

## TP08/09 — Security Login + Roles (Admin/User) with DB

### Goal

Login app with Spring Security + MySQL users table + role-based pages:

- home, login public
    
- user page requires USER/ADMIN
    
- admin page requires ADMIN
    

### Must memorize (security exam)

- Entity `User` mapped to `users` table
    
- `UserRepository.findByUsername`
    
- Create default users at startup (CommandLineRunner)
    
- `CustomUserDetailsService implements UserDetailsService`
    
- Security config rules:
    
    - `/admin/**` → ADMIN
        
    - `/user/**` → USER or ADMIN
        
    - `/` and `/login` → permitAll
        
    - formLogin with custom page
        

#### User entity

```java
@Table(name="users")
public class User {
  private String username;
  private String password;
  private String role;
}
```

#### Repository

```java
public interface UserRepository extends JpaRepository<User, Long> {
  Optional<User> findByUsername(String username);
}
```

#### DataInitializer (default admin/user)

```java
@Component
public class DataInitializer implements CommandLineRunner {
  @Autowired private UserRepository userRepository;
  @Autowired private PasswordEncoder passwordEncoder;

  public void run(String... args){
    if(userRepository.findByUsername("admin").isEmpty()){
      User admin = new User();
      admin.setUsername("admin");
      admin.setPassword(passwordEncoder.encode("admin123"));
      admin.setRole("ROLE_ADMIN");
      userRepository.save(admin);
    }
    if(userRepository.findByUsername("user").isEmpty()){
      User user = new User();
      user.setUsername("user");
      user.setPassword(passwordEncoder.encode("user123"));
      user.setRole("ROLE_USER");
      userRepository.save(user);
    }
  }
}
```

#### CustomUserDetailsService

```java
@Service
public class CustomUserDetailsService implements UserDetailsService {
  @Autowired private UserRepository userRepository;

  @Override
  public UserDetails loadUserByUsername(String username){
    User user = userRepository.findByUsername(username)
      .orElseThrow(() -> new UsernameNotFoundException("User not found: " + username));

    return new org.springframework.security.core.userdetails.User(
      user.getUsername(),
      user.getPassword(),
      AuthorityUtils.createAuthorityList(user.getRole())
    );
  }
}
```

#### Security configuration (classic)

```java
@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

  @Autowired private UserDetailsService userDetailsService;

  @Override
  protected void configure(HttpSecurity http) throws Exception {
    http.authorizeRequests()
      .antMatchers("/admin/**").hasRole("ADMIN")
      .antMatchers("/user/**").hasAnyRole("USER","ADMIN")
      .antMatchers("/", "/login").permitAll()
      .anyRequest().authenticated()
      .and()
      .formLogin().loginPage("/login").permitAll()
      .and()
      .logout().permitAll();
  }

  @Override
  protected void configure(AuthenticationManagerBuilder auth) throws Exception {
    auth.userDetailsService(userDetailsService).passwordEncoder(passwordEncoder());
  }

  @Bean
  public PasswordEncoder passwordEncoder(){
    return new BCryptPasswordEncoder();
  }
}
```

#### Controller pages

```java
@Controller
public class LoginController {
  @GetMapping("/") public String home(){ return "home"; }
  @GetMapping("/login") public String login(){ return "login"; }
  @GetMapping("/user") public String userPage(){ return "user"; }
  @GetMapping("/admin") public String adminPage(){ return "admin"; }
}
```

#### login.html (must know)

```html
<form action="/login" method="post">
  <input type="text" name="username" required>
  <input type="password" name="password" required>
  <button type="submit">Login</button>
</form>
```

---

# 🔥 What I can do next (your “do your thing”)

I can transform each TP into:

1. **One-page cheat sheet** (exam-focused)
    
2. **Flashcards** (QCM style)
    
3. **Fill-the-gap code exercises** (exactly like exams)
    
4. A **mini-project structure** you can copy/paste (packages + files)
    

Tell me which style you want first:

- **A)** “Make me flashcards from TP03–TP05”
    
- **B)** “Make an exam (QCM + code gaps) from Security TP08/09”
    
- **C)** “Give me a full project skeleton (folders + code)”

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DAAW/DAAW|◀ DAAW]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
