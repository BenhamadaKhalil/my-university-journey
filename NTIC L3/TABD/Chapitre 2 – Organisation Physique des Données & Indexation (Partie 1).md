# 🧠 Chapitre 2 – Organisation Physique des Données & Indexation (Partie 1)

👩‍🏫 _Pr. Bouanaka Chafia – Université Constantine 2 (2024/2025 – Semestre 1)_  
📧 _[chafia.bouanaka@univ-constantine2.dz](mailto:chafia.bouanaka@univ-constantine2.dz)_

---

## 🎯 Objectif du cours

Comprendre les **principes et techniques de stockage (التخزين)** des données dans une base de données.

---

## 🗂️ Plan du cours

1. Organisation physique des données (التنظيم الفيزيائي للبيانات)
    
2. Stockage sur disque (التخزين على القرص)
    
3. Traitement des données (معالجة البيانات)
    

---

## 🧩 1. Organisation physique des données (Physical Data Organization)

### 📘 Définition

L’**organisation des données (تنظيم البيانات)** désigne la façon dont les **enregistrements (السجلات)** sont rangés dans un fichier.

> Une base de données est composée d’un ensemble de données stockées sur un **support persistant (وسيط دائم)** — généralement un **disque dur (Hard Disk)**.

🧱 Chaque **fichier (ملف)** correspond à une **table (جدول)** dans la base de données.  
📦 Le SGBD (نظام إدارة قاعدة البيانات) utilise ces fichiers pour stocker les données efficacement.

---

## 💾 2. Enregistrement (Record)

Pour le **système d’exploitation (نظام التشغيل)**, un fichier est juste une **suite d’octets (سلسلة من البايتات)**.  
Mais pour un **SGBD**, c’est plus structuré :  
→ Le fichier est constitué d’**enregistrements** représentant physiquement les **entités (الكيانات)** du modèle.

Selon le modèle logique :

- En SGBD **relationnel** → les enregistrements sont des **tuples (صفوف)**.
    
- En SGBD **orienté objet** → les enregistrements sont des **objets (كائنات)**.
    

Chaque **tuple** contient plusieurs **attributs (خصائص)**,  
et chaque attribut détermine la **taille du champ (حجم الحقل)** nécessaire au stockage.

🧠 Exemple :  
Une table `Client(Nom, Prenom, Age)`  
→ aura un enregistrement avec trois champs (fields) : nom, prénom, âge.

---

## 📦 3. Blocs (Blocks)

### 💡 Définition

Un **bloc (كتلة)** est une **zone mémoire contiguë (منطقة ذاكرة متجاورة)** de taille fixe, stockée sur le disque et **lue/écrite en une seule fois (يتم قراءتها أو كتابتها دفعة واحدة)**.

> ⚙️ Le bloc est **l’unité d’entrée/sortie (وحدة الإدخال والإخراج)** entre la mémoire secondaire (secondary memory) et la mémoire principale (main memory).

---

### 📏 Capacité d’un bloc

Le nombre maximal d’enregistrements (records) qu’un bloc peut contenir :  
[  
\text{Nombre max} = \frac{B}{E}  
]  
où :

- **B** = taille du bloc (block size)
    
- **E** = taille d’un enregistrement (record size)
    

⚠️ Il faut éviter qu’un enregistrement soit **coupé entre deux blocs (منقسم بين كتلتين)**.

---

### 🧩 Types de tuples

Les tuples peuvent être :

- 🔹 **à taille fixe (ثابتة الحجم)**
    
- 🔸 **à taille variable (متغيرة الحجم)**
    

---

## 📘 4. Tuples à taille fixe

Si les données d’un tuple ont des tailles connues et fixes :

> On place simplement les **champs (fields)** les uns derrière les autres.

🧠 Exemple :

```
Tuple (t1, t2, t3)
Taille de chaque champ = d1, d2, d3
=> Enregistrement = [t1][t2][t3]
```

---

## 📗 5. Tuples à taille variable

Quand les champs ont des tailles variables (مثل النصوص الطويلة أو الصور) :  
Plusieurs solutions possibles :

1️⃣ Mettre d’abord les données fixes, puis les données variables précédées d’un **pointeur (مؤشر)** pour localiser la suivante.  
2️⃣ Ou bien, précéder chaque champ variable par **sa taille (حجمه)**.

💡 Le SGBD associe à chaque tuple une **adresse physique (عنوان فيزيائي)** pour le retrouver sur le disque.

---

## ⚙️ 6. Traitement des données (Data Processing)

Quand on veut lire ou modifier une donnée, le système doit :

- 📤 Transférer la donnée du **disque dur (القرص الصلب)** vers la **mémoire principale (الذاكرة الرئيسية)**.
    
- 🕒 Ce transfert prend du **temps important (زمن كبير)** par rapport au calcul en mémoire.
    

💡 C’est le **temps d’accès au disque (زمن الوصول للقرص)** qui ralentit le plus le traitement.

---

## 🚀 7. Le gestionnaire de cache (Cache Manager)

Les SGBD utilisent une **mémoire tampon (ذاكرة مؤقتة)** pour garder une copie temporaire des blocs du disque.  
→ Cela permet de **réduire les lectures/écritures** physiques et d’**accélérer (تسريع)** les accès.

**Paramètres importants :**

- Taille du cache (حجم الذاكرة المؤقتة)
    
- Politique de remplacement (سياسة الاستبدال)
    

📈 Une bonne configuration du cache améliore **l’efficacité du SGBD (كفاءة النظام)**.

---

## 🧾 Résumé global

|Concept (المفهوم)|Définition (التعريف)|Exemple (مثال)|
|---|---|---|
|**Enregistrement (Record)**|Représentation physique d’un tuple (تمثيل فيزيائي للصف)|Client(Nom, Prenom, Age)|
|**Bloc (Block)**|Unité d’entrée/sortie sur disque (وحدة الإدخال والإخراج من القرص)|4 Ko, contient plusieurs tuples|
|**Tuple fixe**|Données de tailles connues (بيانات بحجوم ثابتة)|[Nom][Prenom][Age]|
|**Tuple variable**|Données de tailles différentes (بيانات بحجوم مختلفة)|[Nom][LongText][Image]|
|**Cache**|Mémoire tampon pour accélérer les accès (ذاكرة مؤقتة لتسريع الوصول)|Bloc souvent utilisé stocké en RAM|

---

## 🧠 Points à retenir

- Le stockage sur disque est organisé en **fichiers**, **enregistrements** et **blocs**.
    
- Le bloc est **l’unité d’échange** entre disque et mémoire.
    
- Les tuples peuvent avoir **taille fixe ou variable**.
    
- Le **cache** joue un rôle clé dans la performance du SGBD.
    
- Le **temps d’accès disque** est la principale source de lenteur (البطء).
    

---
# 📏 All Calculation Rules in Chapitre 2 – Partie 1

---

## 🧮 **1. Nombre maximal d’enregistrements dans un bloc**

This is the **only explicit formula** in this chapter:

Nombre maximal d’enregistrements par bloc=BE\text{Nombre maximal d’enregistrements par bloc} = \frac{B}{E}Nombre maximal d’enregistrements par bloc=EB​

Where:

- **B** = taille du bloc (block size in bytes)
    
- **E** = taille d’un enregistrement (record size in bytes)
    

🧠 **Meaning**:  
It tells you how many records fit into a single disk block.

💡 **Example:**  
If a block = 4 Ko (4096 bytes) and each record = 512 bytes →

4096512=8 enregistrements par bloc\frac{4096}{512} = 8 \text{ enregistrements par bloc}5124096​=8 enregistrements par bloc

⚠️ Note:  
We must avoid splitting a record between two blocks (no record should be half in one block and half in another).

---

## ⚙️ **2. (Implicit) Performance Concept – Hit Ratio (نسبة النجاح)**

Even though the formula isn’t explicitly written in Part 1, it’s **implicitly related** to the _cache manager_ concept mentioned at the end.

If you want to measure the cache’s effectiveness:

Hit Ratio=Nombre d’acceˋs trouveˊs dans le cacheNombre total d’acceˋs\text{Hit Ratio} = \frac{\text{Nombre d’accès trouvés dans le cache}}{\text{Nombre total d’accès}}Hit Ratio=Nombre total d’acceˋsNombre d’acceˋs trouveˊs dans le cache​

✅ Higher hit ratio = fewer disk reads = faster performance.

---

## 🧠 Summary Table

| Concept                                       | Formula                                                                                                               | Description                           |
| --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------- |
| **Max records per block**                     | $$N=BEN = \frac{B}{E}N=EB$$​                                                                                          | Number of records stored in one block |
| **Hit ratio (optional, performance measure)** | $$HR=hits in cachetotal accessesHR = \frac{\text{hits in cache}}{\text{total accesses}}HR=total accesseshits in cache | Measures cache efficiency             |

---
# 📏 All Calculation Rules in Chapitre 2 – Partie 1

---

## 🧮 **1. Nombre maximal d’enregistrements dans un bloc**

This is the **only explicit formula** in this chapter:

[  
\text{Nombre maximal d’enregistrements par bloc} = \frac{B}{E}  
]

Where:

- **B** = taille du bloc (block size in bytes)
    
- **E** = taille d’un enregistrement (record size in bytes)
    

🧠 **Meaning**:  
It tells you how many records fit into a single disk block.

💡 **Example:**  
If a block = 4 Ko (4096 bytes) and each record = 512 bytes →  
[  
\frac{4096}{512} = 8 \text{ enregistrements par bloc}  
]

⚠️ Note:  
We must avoid splitting a record between two blocks (no record should be half in one block and half in another).

---

## ⚙️ **2. (Implicit) Performance Concept – Hit Ratio (نسبة النجاح)**

Even though the formula isn’t explicitly written in Part 1, it’s **implicitly related** to the _cache manager_ concept mentioned at the end.

If you want to measure the cache’s effectiveness:
## 🧮 Formules importantes

### 1️⃣ Nombre maximal d’enregistrements dans un bloc
$$
N = \frac{B}{E}
$$
- **B** = taille du bloc (block size)  
- **E** = taille d’un enregistrement (record size)

---

### 2️⃣ Hit Ratio (نسبة النجاح)
$$
HR = \frac{\text{Nombre d’accès trouvés dans le cache}}{\text{Nombre total d’accès}}
$$

🧠 Un **hit ratio** élevé = meilleures performances du SGBD ✅

✅ Higher hit ratio = fewer disk reads = faster performance.

---

## 🧠 Summary Table

| Concept                                       | Formula                                                         | Description                           |
| --------------------------------------------- | --------------------------------------------------------------- | ------------------------------------- |
| **Max records per block**                     | $$( N = \frac{B}{E} )$$                                         | Number of records stored in one block |
| **Hit ratio (optional, performance measure)** | $$( HR = \frac{\text{hits in cache}}{\text{total accesses}} )$$ | Measures cache efficiency             |

---

So:

- ✅ **Only one real calculation** is required in this part (B/E).
    
- 🧩 Everything else is descriptive (definitions, architecture, memory flow, and examples).
    
- ⚙️ The **cache hit ratio** formula is useful if your teacher connects physical storage to performance metrics.
    

---

---
## 🔗 Navigation
- **Module:** [[NTIC L3/TABD/TABD|◀ TABD]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
