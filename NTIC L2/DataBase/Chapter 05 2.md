# Introduction to Normalization

Normalization is the process of organizing a database to minimize redundancy and improve data integrity. It aims to ensure that each fact is stored in only one place, which helps avoid various issues during database evolution. The goal is to separate data into multiple smaller relations, where each relation represents a single semantic concept.

## Key Objectives of Normalization:
- **Minimize redundancy**: Avoid storing the same data in multiple places.
- **Ensure data integrity**: Reduce the risk of anomalies such as update, insertion, and deletion issues.
- **Improve the organization**: Structure data in a way that ensures efficiency and maintainability.

Normalization is based on the concepts of **functional dependencies** and **keys**, and it proceeds through various **normal forms** (1NF, 2NF, 3NF, etc.). The process often involves splitting relations into smaller, more manageable tables.

## Why Normalization is Important:
- It helps in **data consistency** by reducing data duplication.
- It allows the **logical organization** of data, making it easier to update and maintain.
- It prevents issues like **update anomalies** (when the same data is repeated in multiple places) and **deletion anomalies** (when deleting data inadvertently removes important information).

The process of normalization ensures that a database schema is well-structured, leading to better performance and fewer errors in the long run.


# Functional Dependencies and Keys

## 1. **Functional Dependencies (FDs)**

A **Functional Dependency (FD)** is a relationship between two sets of attributes in a relation (table). It signifies that if you know the value of one set of attributes, you can uniquely determine the value of another set.

### Key Points:
- **Notation**: `X → Y`, which means that if you know the value of attributes in set `X`, you can uniquely determine the values of attributes in set `Y`.
- **Attributes in X**: These are called the **determinants**.
- **Attributes in Y**: These are the **dependent attributes**.

### Example:

If `StudentID → Name`, it means knowing the `StudentID` uniquely identifies the `Name` of the student.

- **Functional Dependency Example:**
  - `StudentID → Name`: Knowing a student's `StudentID` determines their `Name`.
  - `RoomID → Capacity`: Knowing the `RoomID` determines the `Capacity` of the room.

### Types of Functional Dependencies:
- **Elementary Functional Dependency**: This is a basic functional dependency where `Y` is a single attribute not included in `X`.
  - Example: `StudentID → Name`
- **Direct Functional Dependency**: A functional dependency `X → Y` is direct if there is no intermediary attribute `Z` such that `X → Z` and `Z → Y`.
  - Example: If `StudentID → RoomID` is not direct because `StudentID → GroupID` and `GroupID → RoomID`.
  - 
### Functional Dependency Example:
```plaintext
| StudentID | Name   | CourseID | RoomID  | Capacity |
|-----------|--------|----------|---------|----------|
| 1         | Alice  | 101      | A01     | 30       |
| 2         | Bob    | 102      | B02     | 25       |

Functional Dependencies:
- `StudentID → Name`
- `RoomID → Capacity`
- `StudentID, CourseID → RoomID`
````

## 2. **Keys**

A **key** is a set of one or more attributes that can uniquely identify a record in a relation (table). There are several types of keys:

### A. **Candidate Key**

- A **candidate key** is a minimal set of attributes that can uniquely identify a record. There may be multiple candidate keys in a relation.
    
    - **Example**: In a `Student` table, both `StudentID` and `Email` can be candidate keys because they both uniquely identify a student.
        

### B. **Primary Key**

- A **primary key** is a candidate key chosen to uniquely identify records in a table. There can only be one primary key in a relation.
    
    - **Example**: `StudentID` can be chosen as the primary key for a `Student` table.
        

### C. **Superkey**

- A **superkey** is any set of attributes that can uniquely identify a record. A superkey may have additional attributes that are not necessary for uniqueness.
    
    - **Example**: `{StudentID, Name}` is a superkey because it uniquely identifies records, but `{StudentID}` alone is sufficient as a candidate key.
        

### D. **Foreign Key**

- A **foreign key** is an attribute or a set of attributes in one table that refers to the primary key in another table. It creates a link between two tables.
    
    - **Example**: In the `Enrollments` table, `StudentID` can be a foreign key that links to the `StudentID` in the `Students` table.
        

### Example of Keys in a Student Table:

```plaintext
| StudentID | Name   | Email             | Department |
|-----------|--------|-------------------|------------|
| 1         | Alice  | alice@email.com    | CS         |
| 2         | Bob    | bob@email.com      | Math       |

Candidate Keys: {StudentID, Email}

Primary Key: StudentID (chosen to uniquely identify each student)
```

## 3. **Functional Dependency and Keys Example**

Let’s take an example of a relation **ExamAssignments** that records which teacher supervises which classroom during an exam:

```plaintext
| TeacherID | RoomID | Task        |
|-----------|--------|-------------|
| T1        | R101   | Chief       |
| T2        | R102   | Assistant   |
| T3        | R101   | Assistant   |

Functional Dependencies:
- `TeacherID → Name, Email`: Knowing `TeacherID` gives you the teacher's `Name` and `Email`.
- `RoomID → Capacity`: Knowing the `RoomID` tells you the `Capacity` of the room.

Keys:
- **Candidate Key**: `{TeacherID, RoomID}`
- **Primary Key**: `TeacherID, RoomID`
- **Foreign Key**: `RoomID` (may link to a `Rooms` table with more details about the room).
```

## 4. **How FDs and Keys are Used in Normalization**

- **Normalization** is based on FDs and keys to eliminate redundancy and improve data integrity.
    
- **1NF, 2NF, and 3NF** use FDs to determine the dependencies between attributes and structure relations accordingly.
    
    - **2NF** addresses **partial dependencies**, ensuring that every non-key attribute is fully functionally dependent on the entire primary key.
        
    - **3NF** resolves **transitive dependencies**, ensuring that non-key attributes are not dependent on other non-key attributes.
        

## Conclusion

Functional dependencies and keys are foundational concepts in relational database design. Understanding them is essential for achieving **normalization**, which minimizes redundancy and improves data integrity.

```

This explanation provides an in-depth look at functional dependencies and keys with clear examples. You can copy and paste this into Obsidian. Let me know if you need further clarifications or examples!
```


# Anomalies Caused by Data Redundancy

Data redundancy in a database occurs when the same data is stored in multiple places. While it might seem harmless at first, redundancy can lead to various problems during data manipulation, especially in larger, evolving databases. These issues are collectively known as **anomalies**.

## Types of Anomalies Caused by Data Redundancy:
```markdown
1. **Update Anomaly**
   - **Description**: This anomaly occurs when data is duplicated across multiple rows. If one instance of the data is updated, all corresponding instances must also be updated, or else the database will become inconsistent.
   - **Example**: Imagine a `Student` table where the teacher's email is stored multiple times:
   
   ```plaintext
   | StudentID | Name   | TeacherID | TeacherEmail        |
   |-----------|--------|-----------|---------------------|
   | 1         | Alice  | T001      | teacher1@email.com  |
   | 2         | Bob    | T001      | teacher1@email.com  |
```

If the teacher's email changes (e.g., to `teacher1@newemail.com`), the update needs to occur in every row where the teacher is assigned. If one row is missed, the database will have conflicting information.

2. **Insertion Anomaly**
    
    - **Description**: An insertion anomaly happens when you are unable to insert new data into the database without providing redundant information.
        
    - **Example**: If we want to add a new teacher without assigning them to any students yet, we may have to insert a row with an empty `StudentID` or other redundant data:
        
    
    ```plaintext
    | StudentID | Name   | TeacherID | TeacherEmail        |
    |-----------|--------|-----------|---------------------|
    | NULL      | NULL   | T002      | teacher2@email.com  |
    ```
    
    This leads to unnecessary redundancy (inserting NULLs) just to include the new teacher. We shouldn't have to insert redundant student information if the teacher is not yet assigned.
    
3. **Deletion Anomaly**
    
    - **Description**: A deletion anomaly occurs when deleting a record results in unintended loss of important information.
        
    - **Example**: Consider a `ClassroomAssignments` table that stores both classroom details and teacher assignments:
        
    
    ```plaintext
    | TeacherID | RoomID | Task    | Floor  | Capacity |
    |-----------|--------|---------|--------|----------|
    | T001      | R101   | Chief   | 1      | 25       |
    | T002      | R102   | Assistant| 2     | 30       |
    ```
    
    If we delete the last assignment for room `R102` (i.e., when `T002` stops teaching), the information about room `R102`—its `Floor` and `Capacity`—is lost:
    
    ```plaintext
    | TeacherID | RoomID | Task    | Floor  | Capacity |
    |-----------|--------|---------|--------|----------|
    | T001      | R101   | Chief   | 1      | 25       |
    ```
    
    Now, if we need to know about `R102`, we have lost that information due to the deletion of the last assignment for that room.
    

## Solutions to Prevent Anomalies:

The primary solution to these anomalies is **normalization**, which involves decomposing tables into smaller, related tables to remove redundancy. By applying normalization rules (1NF, 2NF, 3NF), we ensure that:

- **Each fact is stored in only one place**, preventing the need for repeated data.
    
- We eliminate **partial** and **transitive dependencies**, ensuring data consistency and reducing redundancy.
    

### Example of Normalized Table to Solve Anomalies:

Instead of storing teacher and classroom information in a single table, we split them into separate tables:

```plaintext
Teachers:
| TeacherID | TeacherName     | TeacherEmail        |
|-----------|-----------------|---------------------|
| T001      | Mr. A           | teacher1@email.com  |
| T002      | Mr. B           | teacher2@email.com  |

Classrooms:
| RoomID | Floor | Capacity |
|--------|-------|----------|
| R101   | 1     | 25       |
| R102   | 2     | 30       |

Assignments:
| TeacherID | RoomID | Task      |
|-----------|--------|-----------|
| T001      | R101   | Chief     |
| T002      | R102   | Assistant |
```

- **Teachers** table stores teacher information.
    
- **Classrooms** table stores classroom details.
    
- **Assignments** table links teachers to classrooms and their tasks.
    

Now, if a teacher's email changes, we only need to update it in the **Teachers** table, avoiding an update anomaly. Similarly, if a new teacher is added without assignments, no redundant student or classroom data is required.

## Conclusion

Data redundancy causes **update**, **insertion**, and **deletion** anomalies, which can significantly impact the integrity and consistency of a database. By applying normalization and ensuring each piece of information is stored in only one place, these anomalies can be minimized or eliminated, leading to a more efficient and reliable database design.

```

This markdown version explains the anomalies caused by data redundancy with detailed examples and solutions for avoiding them. You can copy and paste it directly into Obsidian. Let me know if you need further adjustments or more examples!
```


# Normalization Steps

Normalization is a process in database design used to organize a database into smaller, well-structured tables to eliminate redundancy and improve data integrity. The process follows several steps, each corresponding to a **Normal Form (NF)**. 

## 1. **First Normal Form (1NF)**

A table is in **1NF** if:
- All attributes contain atomic (indivisible) values.
- Each column contains only a single value per row (no repeating groups or arrays).
- Each row must be unique.

### Steps to Achieve 1NF:
- Ensure each column holds only atomic values (no lists or sets).
- Remove repeating groups or multi-valued attributes.

### Example:

**Non-1NF Table:**
```plaintext
| StudentID | Name  | Courses                  |
|-----------|-------|--------------------------|
| 1         | Alice | Math, Physics            |
| 2         | Bob   | History, Art             |
````

**Converted to 1NF:**

```plaintext
| StudentID | Name  | Course   |
|-----------|-------|----------|
| 1         | Alice | Math     |
| 1         | Alice | Physics  |
| 2         | Bob   | History  |
| 2         | Bob   | Art      |
```

- The `Courses` column is split into individual rows, and now each cell contains a single value, making the table atomic.
    

## 2. **Second Normal Form (2NF)**

A table is in **2NF** if:

- It is in **1NF**.
    
- Every non-key attribute is **fully functionally dependent** on the entire primary key. No **partial dependencies** (where non-key attributes depend only on part of the primary key).
    

#### Steps to Achieve 2NF:

- Identify the composite primary key.
    
- Remove partial dependencies by moving non-key attributes that depend only on part of the key into separate tables.
    

#### Example:

**Non-2NF Table:**

```plaintext
| StudentID | CourseID | Name   | CourseName |
|-----------|----------|--------|------------|
| 1         | 101      | Alice  | Math       |
| 1         | 102      | Alice  | Physics    |
| 2         | 101      | Bob    | Math       |
```

- `Name` depends only on `StudentID`, and `CourseName` depends only on `CourseID`.
    

**Converted to 2NF:**

- Split the table into `Students`, `Courses`, and `Enrollments`:
    

```plaintext
Students:
| StudentID | Name   |
|-----------|--------|
| 1         | Alice  |
| 2         | Bob    |

Courses:
| CourseID | CourseName |
|----------|------------|
| 101      | Math       |
| 102      | Physics    |

Enrollments:
| StudentID | CourseID |
|-----------|----------|
| 1         | 101      |
| 1         | 102      |
| 2         | 101      |
```

- Now, `Name` is stored only in the `Students` table, and `CourseName` is stored only in the `Courses` table.
    

## 3. **Third Normal Form (3NF)**

A table is in **3NF** if:

- It is in **2NF**.
    
- No non-key attribute depends on another non-key attribute (i.e., there are no **transitive dependencies**).
    

### Steps to Achieve 3NF:

- Identify transitive dependencies (when a non-key attribute depends on another non-key attribute).
    
- Remove these transitive dependencies by creating new relations.
    

### Example:

**Non-3NF Table:**

```plaintext
| StudentID | Name   | Department | DeptHead |
|-----------|--------|------------|----------|
| 1         | Alice  | CS         | Dr. Smith|
| 2         | Bob    | Math       | Dr. Johnson|
```

- `DeptHead` depends on `Department`, not `StudentID`, creating a transitive dependency.
    

**Converted to 3NF:**

```plaintext
Students:
| StudentID | Name   | Department |
|-----------|--------|------------|
| 1         | Alice  | CS         |
| 2         | Bob    | Math       |

Departments:
| Department | DeptHead     |
|------------|-------------|
| CS         | Dr. Smith   |
| Math       | Dr. Johnson |
```

- `DeptHead` is moved to the `Departments` table, removing the transitive dependency.
    

## 4. **Boyce-Codd Normal Form (BCNF)**

A table is in **Boyce-Codd Normal Form (BCNF)** if:

- It is in **3NF**.
    
- For every functional dependency `X → Y`, `X` is a **superkey** (a key that uniquely identifies records).
    

### Steps to Achieve BCNF:

- Check all functional dependencies.
    
- Ensure that every determinant is a superkey. If not, decompose the table further.
    

### Example:

**Non-BCNF Table:**

```plaintext
| StudentID | CourseID | TeacherID |
|-----------|----------|-----------|
| 1         | 101      | T1        |
| 1         | 102      | T2        |
| 2         | 101      | T1        |
```

- `CourseID → TeacherID` is a functional dependency, but `CourseID` is not a superkey.
    

**Converted to BCNF:**

```plaintext
Courses:
| CourseID | TeacherID |
|----------|-----------|
| 101      | T1        |
| 102      | T2        |

Enrollments:
| StudentID | CourseID |
|-----------|----------|
| 1         | 101      |
| 1         | 102      |
| 2         | 101      |
```

- Now, `CourseID → TeacherID` has been handled by separating it into the `Courses` table, ensuring that `CourseID` is a superkey in the `Courses` table.
    

## 5. **Fourth Normal Form (4NF)**

A table is in **4NF** if:

- It is in **BCNF**.
    
- It does not contain **multivalued dependencies**.
    

### Steps to Achieve 4NF:

- Identify any multivalued dependencies (when one attribute determines multiple values of other attributes).
    
- Decompose the table to remove multivalued dependencies.
    

## 6. **Fifth Normal Form (5NF)**

A table is in **5NF** if:

- It is in **4NF**.
    
- It does not contain any **join dependencies**.
    

### Steps to Achieve 5NF:

- Decompose relations further if needed to remove join dependencies, ensuring that all data is stored in its most granular form.
    

## Conclusion

Normalization is a systematic approach to organizing a database to eliminate redundancy and improve data integrity. By following the steps for each normal form, starting from **1NF** to **5NF**, a database can be designed to be both efficient and flexible for future modifications.

```

This explanation provides a clear breakdown of each normalization step with examples. You can copy and paste this directly into Obsidian. Let me know if you need further clarification!
```


# Decomposition Process

The **decomposition process** in database normalization involves breaking down a large, unnormalized relation into smaller, well-structured relations while preserving the original information and functional dependencies (FDs). This process is essential for achieving higher normal forms like **2NF**, **3NF**, and **BCNF**, and it ensures that the resulting relations are **lossless** and **dependency-preserving**.

## Key Concepts in Decomposition:
1. **Lossless Join**: A decomposition is lossless if the original relation can be reconstructed by performing a **natural join** on the decomposed relations without losing any information.
2. **Dependency-Preserving**: A decomposition is dependency-preserving if all functional dependencies from the original relation are preserved in the decomposed relations.

## Steps in the Decomposition Process:

### Step 1: Identify the Functional Dependencies
- Begin by analyzing the original relation and identifying all functional dependencies (FDs).
- Ensure that each FD is well understood and its impact on the schema is clear.

### Step 2: Decompose the Relation Based on FDs
- The goal of decomposition is to break down the relation into smaller relations that:
  - **Eliminate redundancy**.
  - **Preserve all FDs**.
  - **Ensure a lossless-join**.
  
- Decompose the relation by creating new tables for each subset of attributes that functionally determine other attributes.

### Example:

Consider a relation `R(StudentID, CourseID, TeacherID, TeacherName)` with the following functional dependencies:
- `StudentID → TeacherID, TeacherName`
- `CourseID → TeacherID`
- `StudentID, CourseID → TeacherName`

##### Original Table (Non-normalized):
```plaintext
| StudentID | CourseID | TeacherID | TeacherName |
|-----------|----------|-----------|-------------|
| 1         | 101      | T1        | Dr. Smith   |
| 1         | 102      | T2        | Dr. Johnson |
| 2         | 101      | T1        | Dr. Smith   |
````

- The `TeacherName` depends on `TeacherID`, but `TeacherID` also depends on `CourseID` and `StudentID`.
    

### Step 3: Perform Decomposition

- **Decompose into two relations** to eliminate redundancy:
    

```plaintext
Teachers:
| TeacherID | TeacherName |
|-----------|-------------|
| T1        | Dr. Smith   |
| T2        | Dr. Johnson |

Enrollments:
| StudentID | CourseID | TeacherID |
|-----------|----------|-----------|
| 1         | 101      | T1        |
| 1         | 102      | T2        |
| 2         | 101      | T1        |
```

- Now, `TeacherName` is stored only once in the `Teachers` table, and `TeacherID` is used as a reference in the `Enrollments` table.
    

### Step 4: Ensure Lossless Join and Dependency Preservation

- **Lossless Join**: We can reconstruct the original `TeacherName` in the `Enrollments` table by joining the `Teachers` and `Enrollments` tables on `TeacherID`. This ensures no data is lost during decomposition.
    

```sql
SELECT E.StudentID, E.CourseID, T.TeacherName
FROM Enrollments E
JOIN Teachers T ON E.TeacherID = T.TeacherID;
```

- **Dependency Preservation**: All functional dependencies are preserved:
    
    - `StudentID → TeacherID, TeacherName` is preserved by the `Enrollments` and `Teachers` relation.
        
    - `CourseID → TeacherID` is preserved in the `Enrollments` relation.
        

### Step 5: Repeat the Process if Necessary

- If the relations are not yet in the desired normal form (e.g., if partial or transitive dependencies still exist), repeat the decomposition process.
    

## Example of Lossless-Join and Dependency-Preserving Decomposition:

Let’s say we have a relation `R(A, B, C, D)` with functional dependencies `A → B`, `B → C`, and `C → D`.

1. **Initial Table**: `R(A, B, C, D)`
    
2. **Decompose**:
    
    - `R1(A, B)` based on `A → B`.
        
    - `R2(B, C)` based on `B → C`.
        
    - `R3(C, D)` based on `C → D`.
        

Now, the decomposition ensures that the data can be reconstructed by performing a **natural join** between `R1`, `R2`, and `R3`.

## Conclusion

The decomposition process is a crucial step in database normalization, ensuring that a relational schema is both efficient and free from redundancy while preserving the functional dependencies. By following the steps of decomposition, a database designer ensures that the resulting schema is lossless and dependency-preserving, ultimately leading to a more reliable and maintainable database.

```

This explanation provides a step-by-step guide to the decomposition process, detailing the concepts of lossless join, dependency preservation, and the overall benefits of normalization. You can paste this directly into Obsidian. Let me know if you need any further adjustments!
```
# Synthesis Algorithm

The **Synthesis Algorithm** is a systematic method used to decompose a relation into **Third Normal Form (3NF)** while ensuring that the decomposition is both **lossless-join** and **dependency-preserving**. The algorithm ensures that all functional dependencies (FDs) from the original relation are preserved in the decomposed relations, and the original relation can be reconstructed through natural joins without any loss of information.

## Key Concepts in Synthesis:
1. **Lossless Join**: A decomposition is lossless if we can reconstruct the original relation from the decomposed relations without any loss of data.
2. **Dependency-Preserving**: A decomposition is dependency-preserving if all functional dependencies from the original relation are preserved in the decomposed relations.
3. **3NF**: A relation is in **Third Normal Form (3NF)** if it is in 2NF and there are no transitive dependencies between non-key attributes.

## Steps of the Synthesis Algorithm:

### Step 1: Find a Minimal Cover for Functional Dependencies
- A **minimal cover** of functional dependencies is the simplest set of functional dependencies that are equivalent to the original set of FDs.
- To find the minimal cover, perform the following steps:
  1. **Remove extraneous attributes**: If any attribute on the left-hand side of a functional dependency can be removed without changing the dependency, remove it.
  2. **Remove redundant dependencies**: If a dependency can be derived from the other dependencies, remove it.

### Step 2: Create a Relation for Each Functional Dependency
- For each functional dependency `X → Y` in the minimal cover, create a relation with `X` as the primary key and all attributes of `Y` included.
  - **Example**: If `A → B` is a functional dependency, create a relation with `A` as the primary key and `B` as the attribute.

### Step 3: Ensure All Relations are in 3NF
- The relations created in Step 2 must be in 3NF. A relation is in 3NF if:
  - It is in 2NF.
  - For every functional dependency `X → Y`, either:
    - `X` is a superkey, or
    - `Y` is a prime attribute (part of a candidate key).

### Step 4: Combine Relations with Common Attributes
- If two or more relations have the same set of attributes, they should be combined to avoid redundancy. The relations are merged based on the common attributes, ensuring that they are still in 3NF.

### Example of the Synthesis Algorithm:

Let's consider a relation `R(A, B, C, D)` with the following functional dependencies:
- `A → B`
- `B → C`
- `A → D`

#### Step 1: Find a Minimal Cover for the FDs

- **Remove extraneous attributes**:
  - The dependency `A → B` is minimal, so we leave it as is.
  - `B → C` is also minimal.
  - `A → D` is already minimal.

- **Minimal cover**: The minimal cover is the same as the original set of dependencies: `{A → B, B → C, A → D}`.

#### Step 2: Create a Relation for Each Functional Dependency

From the minimal cover, create relations for each functional dependency:

1. `R1(A, B)` for `A → B`
2. `R2(B, C)` for `B → C`
3. `R3(A, D)` for `A → D`

#### Step 3: Ensure All Relations are in 3NF

- **Relation R1(A, B)**: `A → B`. Here, `A` is a superkey, so `R1` is in 3NF.
- **Relation R2(B, C)**: `B → C`. `B` is the primary key in `R2`, so `R2` is in 3NF.
- **Relation R3(A, D)**: `A → D`. `A` is a superkey, so `R3` is in 3NF.

#### Step 4: Combine Relations with Common Attributes

- Relations `R1(A, B)` and `R3(A, D)` share the attribute `A`, so they are already combined in this case.

#### Final Relations (in 3NF):
- `R1(A, B)`
- `R2(B, C)`
- `R3(A, D)`

Now, all functional dependencies are preserved, and the relations are in **3NF**.

## Conclusion
The Synthesis Algorithm is an effective method for decomposing a relation into 3NF while ensuring that the decomposition is **lossless** and **dependency-preserving**. This algorithm helps database designers structure data efficiently, avoiding redundancy and anomalies while ensuring data integrity.


# Key Concepts in Database Design

## 1. **Functional Dependency (FD)**

A **functional dependency (FD)** is a relationship between two sets of attributes in a database relation. It signifies that the value of one set of attributes (called the **determinant**) uniquely determines the value of another set of attributes (called the **dependent** attributes).

### Notation:
- **X → Y**: "X determines Y" or "Y is functionally dependent on X."
- **Example**: If `StudentID → Name`, knowing the `StudentID` will uniquely determine the `Name` of the student.

### Types of Functional Dependencies:
- **Direct Functional Dependency**: A functional dependency `X → Y` is **direct** if there is no intermediary attribute `Z` such that `X → Z` and `Z → Y`.
- **Transitive Dependency**: A functional dependency `X → Y` is **transitive** if `X → Z` and `Z → Y` exist, and `X` is not directly determining `Y`.

### Example:
- `StudentID → Name`: Knowing `StudentID` will give you the `Name`.
- `TeacherID → TeacherName`: Knowing `TeacherID` will give you the `TeacherName`.

---

## 2. **Key**

A **key** is a set of one or more attributes that can uniquely identify a tuple (row) in a relation (table). Keys are essential for establishing relationships between tables and ensuring data integrity.

### Types of Keys:

- **Candidate Key**:
  - A **candidate key** is a minimal set of attributes that uniquely identifies a record in a table. There can be multiple candidate keys for a relation.
  - **Example**: In a `Student` table, both `StudentID` and `Email` could be candidate keys, as each uniquely identifies a student.

- **Primary Key**:
  - A **primary key** is a candidate key chosen to uniquely identify records in a table. There is only one primary key in a relation.
  - **Example**: `StudentID` could be selected as the primary key for the `Student` table.

- **Superkey**:
  - A **superkey** is any set of attributes that can uniquely identify a record in a table. A superkey may include additional attributes beyond what is necessary to uniquely identify a record.
  - **Example**: `{StudentID, Name}` is a superkey, as it uniquely identifies a record, but `{StudentID}` alone is sufficient.

- **Foreign Key**:
  - A **foreign key** is an attribute or set of attributes in one table that references the primary key in another table. It establishes a relationship between the two tables.
  - **Example**: In an `Enrollments` table, `StudentID` can be a foreign key that links to `StudentID` in the `Students` table.

---

## 3. **Normalization**

**Normalization** is the process of organizing a database schema to reduce redundancy and dependency. The goal of normalization is to ensure that each piece of information is stored only once, which improves data integrity and efficiency.

### Normal Forms (NF):
- **1NF (First Normal Form)**: Ensures all attributes are atomic (indivisible), with no repeating groups.
- **2NF (Second Normal Form)**: Builds on 1NF and removes partial dependencies (where non-key attributes depend on part of the primary key).
- **3NF (Third Normal Form)**: Builds on 2NF and removes transitive dependencies (where non-key attributes depend on other non-key attributes).
- **BCNF (Boyce-Codd Normal Form)**: A stricter version of 3NF where every determinant is a superkey.

### Example:
Given a `Student` table:
```plaintext
| StudentID | Name  | CourseID | TeacherName |
|-----------|-------|----------|-------------|
| 1         | Alice | 101      | Mr. Smith   |
| 2         | Bob   | 102      | Mrs. Johnson|
````

- **1NF**: Split multi-valued fields into separate rows.
    
- **2NF**: Remove partial dependency by separating `Student` and `Course` data.
    
- **3NF**: Remove transitive dependency by placing `TeacherName` in a separate table.
    

---

## 4. **Lossless Join**

A **lossless join** is a property of a decomposition where the original relation can be reconstructed by joining the decomposed relations without losing any data.

- This property is essential in **normalization**, ensuring that decomposing a relation does not lead to the loss of information.
    
- The decomposition is lossless if a **natural join** between the decomposed relations yields the original relation.
    

### Example:

- If you decompose the `Student` table into `Students(StudentID, Name)` and `Enrollments(StudentID, CourseID)`, you can reconstruct the original `Student` table by performing a **natural join** on `StudentID`.
    

---

## 5. **Dependency Preservation**

**Dependency preservation** means that all functional dependencies (FDs) of the original relation are preserved in the decomposed relations.

- Ensuring dependency preservation is crucial in normalization because it helps maintain the integrity of the database when updating data. If dependencies are preserved, the database can be modified without violating any integrity constraints.
    

### Example:

- If a relation `R(A, B, C)` has the FD `A → B`, then after decomposition into two relations `R1(A, B)` and `R2(A, C)`, the dependency `A → B` must still hold in `R1` to preserve the integrity of the original relation.
    

---

## 6. **Superkey and Candidate Key**

A **superkey** is a set of attributes that can uniquely identify a record in a relation. A **candidate key** is a minimal superkey, meaning it has no extraneous attributes.

- **Superkey**: `{StudentID, Name}` (can uniquely identify a student, but `{StudentID}` alone is sufficient).
    
- **Candidate Key**: `{StudentID}` (minimal set that uniquely identifies a student).
    
- **Primary Key**: `{StudentID}` (chosen from the candidate keys to uniquely identify each student record).
    

---

## Conclusion

**Functional dependencies** and **keys** are foundational concepts in relational database design. Understanding these concepts is crucial for achieving **normalization**, ensuring that data is organized efficiently and without redundancy. By applying these principles, database designers can build databases that maintain **data integrity**, **eliminate redundancy**, and are **easier to manage** as they grow.

```

This section explains **Functional Dependencies** and **Keys** in detail, with examples that should be easy to paste into Obsidian for reference. Let me know if you need more examples or further clarification!
```


# Example Case: Teacher Assignment to Classroom

In this example, we are going to use a **Teacher Assignment** scenario to demonstrate the process of normalization and how functional dependencies (FDs) and keys are used to organize data. We will walk through the steps of normalizing a database schema, starting from an unnormalized relation and moving through the normal forms (1NF, 2NF, 3NF).

## Initial Data (Unnormalized Table)
We begin with a relation that stores information about teachers, classrooms, and their assignments for exams:

```plaintext
| TeacherID | TeacherName | TeacherEmail         | Classroom | Floor | Capacity | Task       |
|-----------|-------------|----------------------|-----------|-------|----------|------------|
| T001      | Mr. Smith   | mr.smith@email.com    | R101      | 1     | 25       | Chief      |
| T002      | Mrs. Johnson| mrs.johnson@email.com | R102      | 2     | 30       | Assistant  |
| T003      | Dr. Brown   | dr.brown@email.com    | R101      | 1     | 25       | Assistant  |
| T001      | Mr. Smith   | mr.smith@email.com    | R103      | 1     | 20       | Chief      |
````

### Functional Dependencies:

- `TeacherID → TeacherName, TeacherEmail`: Knowing `TeacherID` gives us the `TeacherName` and `TeacherEmail`.
    
- `Classroom → Floor, Capacity`: Knowing the `Classroom` number determines the `Floor` and `Capacity`.
    
- `TeacherID, Classroom → Task`: A combination of `TeacherID` and `Classroom` determines the `Task` (Chief or Assistant).
    

## 1. **First Normal Form (1NF)**

To achieve **1NF**, we need to ensure that all columns contain atomic values (i.e., no repeating groups).

In the original table, the data is already atomic, so there are no multi-valued attributes. The table is in **1NF**. However, there is redundancy due to the repetition of `TeacherName`, `TeacherEmail`, `Floor`, and `Capacity` for each teacher's assignment to different classrooms.

## 2. **Second Normal Form (2NF)**

To achieve **2NF**, we need to remove **partial dependencies**, which occur when a non-key attribute is dependent on only part of the primary key. In this case, `TeacherName` and `TeacherEmail` depend only on `TeacherID`, and `Floor` and `Capacity` depend only on `Classroom`, not on the full composite key (`TeacherID`, `Classroom`).

### Decomposition into 2NF:

We decompose the table into three separate tables:

- **Teachers Table**: Stores teacher information.
    
- **Classrooms Table**: Stores classroom information.
    
- **Assignments Table**: Stores the assignments of teachers to classrooms.
    

```plaintext
Teachers:
| TeacherID | TeacherName | TeacherEmail        |
|-----------|-------------|---------------------|
| T001      | Mr. Smith   | mr.smith@email.com   |
| T002      | Mrs. Johnson| mrs.johnson@email.com|
| T003      | Dr. Brown   | dr.brown@email.com   |

Classrooms:
| Classroom | Floor | Capacity |
|-----------|-------|----------|
| R101      | 1     | 25       |
| R102      | 2     | 30       |
| R103      | 1     | 20       |

Assignments:
| TeacherID | Classroom | Task      |
|-----------|-----------|-----------|
| T001      | R101      | Chief     |
| T002      | R102      | Assistant |
| T003      | R101      | Assistant |
| T001      | R103      | Chief     |
```

Now, the **Teachers Table** stores teacher details, the **Classrooms Table** stores classroom details, and the **Assignments Table** stores the assignment information, removing partial dependencies.

## 3. **Third Normal Form (3NF)**

To achieve **3NF**, we need to ensure that there are **no transitive dependencies** (i.e., non-key attributes that depend on other non-key attributes). In the **Teachers Table**, `TeacherID` is the primary key, and `TeacherName` and `TeacherEmail` depend directly on `TeacherID`. There are no transitive dependencies, so the tables are already in **3NF**.

### Final Normalized Schema:

- **Teachers Table**: Stores teacher information.
    
- **Classrooms Table**: Stores classroom details.
    
- **Assignments Table**: Stores teacher assignments to classrooms with their tasks.
    

```plaintext
Teachers:
| TeacherID | TeacherName | TeacherEmail        |
|-----------|-------------|---------------------|
| T001      | Mr. Smith   | mr.smith@email.com   |
| T002      | Mrs. Johnson| mrs.johnson@email.com|
| T003      | Dr. Brown   | dr.brown@email.com   |

Classrooms:
| Classroom | Floor | Capacity |
|-----------|-------|----------|
| R101      | 1     | 25       |
| R102      | 2     | 30       |
| R103      | 1     | 20       |

Assignments:
| TeacherID | Classroom | Task      |
|-----------|-----------|-----------|
| T001      | R101      | Chief     |
| T002      | R102      | Assistant |
| T003      | R101      | Assistant |
| T001      | R103      | Chief     |
```

## Conclusion

The original **Teacher Assignment** table was decomposed into three smaller tables to achieve normalization:

- **1NF**: Ensured atomic values in each column.
    
- **2NF**: Removed partial dependencies by creating separate tables for teachers, classrooms, and assignments.
    
- **3NF**: Ensured no transitive dependencies, resulting in a clean and efficient schema.
    

Normalization has resolved issues of **data redundancy**, **update anomalies**, and **insertion anomalies**, leading to a more efficient and maintainable database design.

```

This example case illustrates how to normalize a database schema through the different normal forms, starting from an unnormalized relation and progressing to **3NF**. You can copy this directly into Obsidian for easy reference. Let me know if you'd like any adjustments or further details!
```

---
## 🔗 Navigation
- **Module:** [[DataBase|◀ DataBase]]
- **Semester:** [[NTIC L2|◀ NTIC L2]]
- **Academic Home:** [[README|🏠 Home]]
