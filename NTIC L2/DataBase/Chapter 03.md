# General Overview

Relational algebra is based on set theory and provides formal operations on relations (tables) to create new relations. It is foundational for managing databases, including systems like SQL.

Relational algebra consists of a set of operations that can be performed on relations (tables) to manipulate and retrieve data. These operations form the theoretical foundation for SQL and other database query languages. Through operations such as selection, projection, and joins, relational algebra allows the creation of new relations from existing ones. These operations are primarily used for querying and managing relational databases efficiently.

### Key Points:
- Relational algebra involves mathematical operations on relations (tables).
- It is foundational for modern relational database management systems (RDBMS).
- The operations help in querying and manipulating data within the database.

# Types of Operations

## Unary Operations

Unary operations involve a single relation (table). The result of these operations is a new relation formed by applying the operation to the original relation.

### 1. **Selection (σ)**
- **Description**: Filters tuples (rows) based on a specified condition.
- **Example**: Selecting all students who are enrolled in a course with a grade 'A'.
  
```plaintext
σ(grade = 'A')(Enrollments)
```

- **Output**: A new relation containing only the students with grade 'A'.
    

### 2. **Projection (π)**

- **Description**: Selects a subset of columns (attributes) from a relation.
    
- **Example**: Projecting only the `Name` and `Major` attributes from the `Students` table.
  π(Name, Major)(Students)
- **Output**: A new relation with only the `Name` and `Major` columns.
    

#### 3. **Renaming (ρ)**

- **Description**: Renames the relation or its attributes.
    
- **Example**: Renaming the `Enrollments` table to `Registrations`.

ρ(Registrations)(Enrollments)

- **Output**: A new relation where the `Enrollments` relation is now called `Registrations`.
    

These unary operations help manipulate data within a single relation by filtering, projecting, or renaming attributes.

Now you can copy the entire section at once. Let me know if you need anything else!

---
## 🔗 Navigation
- **Module:** [[DataBase|◀ DataBase]]
- **Semester:** [[NTIC L2|◀ NTIC L2]]
- **Academic Home:** [[README|🏠 Home]]
