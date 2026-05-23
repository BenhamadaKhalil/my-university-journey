# Indexing & Storage – Rules Summary

## 1. Files, Records, and Blocks

### 1.1 Records per block

```
bfr = floor(B / R)
```

B = block/page size  
R = record size

### 1.2 Number of blocks needed

```
b = ceil(r / bfr)
```

r = number of records

### 1.3 Binary search cost in ordered file

```
Cost = ceil(log2(b))
```

---

## 2. Page Utilization (Occupancy Rate)

If occupancy = u (example: 0.75):

### 2.1 Effective usable space

```
UsableSpace = u * PageSize
```

### 2.2 Records per page with occupancy

```
RecordsPerPage = floor(UsableSpace / R)
```

### 2.3 Number of pages

```
Pages = ceil(r / RecordsPerPage)
```

---

## 3. Sequential Read Time

If:  
P = number of pages  
t = track read time

### Sequential read time

```
TotalTime = P * t
```

---

## 4. Indexes

### 4.1 Dense Index

One entry per record.

```
N1 = r
```

### 4.2 Sparse Index

One entry per block.

```
N1 = b
```

### 4.3 Index entry size

If key = K bytes, pointer = P bytes:

```
IndexEntry = K + P
```

### 4.4 Entries per index page

If occupancy = u:

```
Usable = u * PageSize
EntriesPerPage = floor(Usable / IndexEntry)
```

### 4.5 Index pages needed

```
IndexPages = ceil(N1 / EntriesPerPage)
```

---

## 5. Primary Index

- Built on ordered file.
    
- Sparse index.
    
- Ordered by primary key.
    
- Efficient for range queries.
    

---

## 6. Secondary Index

- Not based on file ordering.
    
- Dense index.
    
- Good for search on non-primary attributes.
    

---

## 7. Composite Index

Index(A, B) optimizes:

- Queries on A
    
- Queries on (A,B)

---
## 🔗 Navigation
- **Module:** [[NTIC L3/TABD/TABD|◀ TABD]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
