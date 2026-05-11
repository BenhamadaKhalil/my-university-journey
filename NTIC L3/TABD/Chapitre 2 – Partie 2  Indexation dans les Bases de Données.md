# 📘 Chapitre 2 – Partie 2

## Organisation Physique des Données & Indexation dans les Bases de Données

_(Full Summary + All Calculation Rules)_

---

## 🎯 Objectifs

- Comprendre les **principes de l’indexation (الفهرسة)**  
- Appliquer les **techniques d’indexation** dans une BD  

---

## 🧠 1. Notion d’Index

Un **index (فهرس)** est une **structure de données** qui améliore la vitesse d’accès aux enregistrements dans une table sans la parcourir entièrement.

### 🔹 Définitions :

| Terme | Description |
|-------|--------------|
| **Clé d’indexation** | Attribut(s) servant à identifier la donnée recherchée |
| **Adresse** | Emplacement du bloc ou de l’enregistrement sur disque |
| **Entrée d’index** | `[valeur, adresse]` – une valeur clé et l’adresse du bloc contenant la donnée |

---

## ⚙️ 2. Typologie des Index

### 🔸 Index primaire (Primary Index)
- Basé sur la clé primaire.  
- Le fichier de données est **ordonné** selon cette clé.  

L’index primaire est souvent **clairsemé (sparse index)** :

- Il **ne contient pas une entrée pour chaque enregistrement**,
    
- mais **une entrée par bloc (page)** de données.

Création :automatique quand on définit une clé primaire
### 🔸 Index secondaire (Secondary Index)
- Utilisé sur les **champs non clés**.  
- Indépendant de l’ordre du fichier.  
- Si on veut souvent chercher par **Nom**, on crée un **index secondaire** :`CREATE INDEX idx_nom ON etudiant(nom);`
Si plusieurs étudiants ont le même nom,  
➡️ l’index secondaire contient **plusieurs adresses** pour une même valeur :

| **Nom** | **Adresses**   |
| ------- | -------------- |
| Ali     | [Bloc1, Bloc4] |
| Karim   | [Bloc2]        |
| Sara    | [Bloc3, Bloc5] |
Structure  généralement **dense** (une entrée par enregistrement)


### 🔸 Index dense (Dense Index)
- Une **entrée d’index par enregistrement**  
🧮 **Nombre d’entrées = nombre d’enregistrements**
#### Principe

- L’index contient **la valeur de l’attribut indexé**  
    **+** l’**adresse physique (pointeur)** vers l’enregistrement correspondant.
    
- Comme chaque enregistrement est représenté,  
    la recherche est **très rapide**,  
    mais l’index **prend plus de place**.
### 🔸 Index non-dense (Sparse Index)
- Une **entrée d’index par bloc**  
🧮 **Nombre d’entrées = nombre de blocs**

---

## 🧮 3. Formule de densité d’un index

$$
\text{Densité d’un Index} = \frac{\text{Nombre de clés dans l’index}}{\text{Nombre total d’enregistrements dans le fichier}}
$$

- Si Densité = 1 → Index dense  
- Si Densité < 1 → Index non-dense  

📘 Exemple :
$$
\text{Densité} = \frac{1000}{10000} = 0.1 \Rightarrow \text{Index non-dense}
$$

---

## 🪵 4. Structures d’Index : Arbres (Trees)

### 🌳 Arbre B (B-Tree)
- Arbre équilibré → profondeur minimale  
- Chaque **nœud interne** contient **k clés** avec :
$$
\text{Ordre de l’arbre} = m
$$
$$
2 \leq k \leq 2m
$$
                   [30 | 60]
                  /     |     \
          [10 | 20]   [40 | 50]   [70 | 80 | 90]

### 🌿 Arbre B+ (B+ Tree)
- Données uniquement dans les **feuilles**  
- Tous les **chemins de la racine aux feuilles** ont la même longueur (équilibré)  
- Chaque **nœud interne** contient :
$$
\text{k clés et (k+1) pointeurs}
$$
- Chaque **nœud feuille** contient les valeurs réelles + pointeur suivant (chaînage)

---

### ⚙️ Opérations sur arbre B+ :

| Opération | Description | Conséquence |
|------------|--------------|-------------|
| **Recherche (بحث)** | Descendre l’arbre jusqu’à la feuille | Logarithmique : `O(log n)` |
| **Insertion (إدراج)** | Si nœud plein → éclatement (split) | Clé médiane remonte |
| **Suppression (حذف)** | Si vide → fusion (merge) ou emprunt | Peut réduire la hauteur |

---
# 📘 **Hachage (Hashing – التجزئة)**

## 🔹 Définition

Le **hachage** est une **méthode d’accès direct** aux enregistrements d’un fichier.  
Elle permet de **trouver une donnée très rapidement**, **sans passer par un arbre ni un index trié**.

> 💡 Le principe :  
> on applique une **fonction de hachage (hash function)** sur la **clé de recherche**,  
> qui donne **l’adresse du bloc** où se trouve l’enregistrement.

---

## 🔹 Principe de fonctionnement

1. Chaque **enregistrement** a une **clé** (ex : N° étudiant, matricule, etc.)
    
2. On applique une **fonction de hachage H(clé)**  
    → cette fonction calcule **l’adresse du bloc** où stocker ou chercher la donnée.
    

```
Adresse = H(clé)
```

---

### 🧩 Exemple simple

Supposons un fichier avec **10 blocs** (0 à 9).

|Clé|Fonction de hachage|Adresse|
|---|---|---|
|123|H(123) = 123 mod 10|3|
|456|H(456) = 456 mod 10|6|
|789|H(789) = 789 mod 10|9|
|159|H(159) = 159 mod 10|9 ← ⚠ collision !|

> Ici, les clés **789** et **159** ont produit la même adresse (9).  
> Cela s’appelle une **collision (تصادم)**.

---

## 🔹 Les collisions

Une **collision** arrive quand **plusieurs clés ont la même adresse de hachage**.  
C’est inévitable — il faut donc une **stratégie pour les gérer**.

---

## 🔹 Méthodes de résolution des collisions

| Méthode                                 | Principe                                                                                           |
| --------------------------------------- | -------------------------------------------------------------------------------------------------- |
| **Chaînage (chaining)**                 | Chaque case de la table pointe vers une **liste chaînée** d’enregistrements ayant la même adresse. |
| **Adressage ouvert (open addressing)**  | On cherche une **autre case libre** selon une règle (linéaire, quadratique…).                      |
| **Zone de débordement (overflow area)** | On garde une **zone spéciale** pour stocker les enregistrements en trop.                           |

---

## 🔹 Exemple visuel (hachage + collision)

```
Table principale :
Index : 0 1 2 3 4 5 6 7 8 9
Valeur:   - - - A - - B - - -

Zone de débordement :
[ A2, B2, B3 ]
```

→ Si deux clés donnent le même index, le **premier** est stocké dans le bloc,  
et les **suivants** vont dans la **zone de débordement**.

---

## 🔹 Types de hachage

|Type|Description|
|---|---|
|**Hachage statique**|La taille de la table est **fixe** (ne change jamais). Simple mais peut vite se saturer.|
|**Hachage dynamique**|La taille de la table **s’adapte automatiquement** quand elle devient trop pleine. (Ex : **hachage extensible** ou **hachage linéaire**)|

---

## 🔹 Comparaison : Hachage vs Indexation (B+ Tree)

|Critère|**Hachage**|**B+ Tree**|
|---|---|---|
|**Principe**|Calcul direct de l’adresse|Parcours d’un arbre équilibré|
|**Données triées ?**|❌ Non|✅ Oui|
|**Accès exact (clé connue)**|⚡ Très rapide|Rapide|
|**Recherche par intervalle (ex : 10 < x < 20)**|❌ Impossible|✅ Possible|
|**Gestion de mise à jour**|Difficile|Facile|
|**Utilisation typique**|Accès direct à un enregistrement|Requêtes avec tri, intervalles, etc.|

---

## 🔹 Schéma simplifié du hachage

```
          +-------------------+
Clé  ---> | Fonction H(clé)   | ---> Adresse du bloc
          +-------------------+
                       ↓
          +-------------------+
          | Bloc dans le fichier |
          +-------------------+
```

---

## 🧠 En résumé

|Élément|Description|
|---|---|
|**Nom complet**|Hashing / التجزئة|
|**But**|Accès direct rapide aux enregistrements|
|**Principe**|Calculer une adresse via une fonction de hachage|
|**Collision**|Quand 2 clés donnent la même adresse|
|**Types**|Statique / Dynamique|
|**Complexité d’accès**|O(1) moyenne|
|**Utilisé pour**|Requêtes exactes (clé connue)|

---

## 🧮 6. Gestion du Cache et des Blocs

Lorsqu’un SGBD lit une donnée :
- Si le bloc est déjà dans le **cache mémoire (الذاكرة المؤقتة)** → accès rapide ✅  
- Sinon → lecture disque lente ❌  

### 🔹 Objectif :
Maximiser le **Hit Ratio (نسبة النجاح)**
$$
\text{Hit Ratio} = \frac{\text{Nombre d’accès trouvés en cache}}{\text{Nombre total d’accès}}
$$
_Un bon SGBD cherche à avoir un hit ratio élevé → moins d’accès disque._

---

## 💡 7. Index Bitmap (فهرس بتّي)

Structure sous forme de **tableau binaire (binary matrix)**  
- Colonnes → valeurs possibles de la clé  
- Lignes → enregistrements  
- 1 = présence ; 0 = absence  

### Exemple :

| Nom | Sexe | Situation |
|-----|------|-----------|
| Ali | M | Marié |
| Aya | F | Célibataire |

**Bitmap pour Sexe :**

|   | M | F |
|---|---|---|
| Ali | 1 | 0 |
| Aya | 0 | 1 |

🧮 **Requête logique (requête booléenne)** :
```sql
SELECT * FROM Personne
WHERE sexe='M' AND situation='Marié';
````

→ Combinaison de deux bitmaps avec une opération **AND** (و).

---

## 📘 8. Calculs et Formules à retenir (ملخص القوانين)

|Concept|Formule|Traduction|
|---|---|---|
|**Densité d’un Index**|`D = (Nb_clés_index / Nb_enregistrements)`|كثافة الفهرس|
|**Adresse relative (hachage statique)**|`AR = N × L`|العنوان النسبي|
|**Hit Ratio (cache)**|`HR = (Accès_cache / Accès_total)`|نسبة نجاح الوصول في الذاكرة|
|**Capacité d’un bloc**|`Nb_enregistrements_max = B / E`|عدد السجلات في كتلة واحدة|
|**Complexité recherche arbre B/B+**|`O(log n)`|التعقيد اللوغاريتمي|

---

✅ **En résumé :**

- Un **index** réduit le coût des recherches.
    
- Les **arbres B+** équilibrent les accès.
    
- Le **hachage** offre un accès direct.
    
- Les **bitmaps** sont utiles pour les requêtes logiques.
    
- Les **formules** ci-dessus servent pour mesurer la performance ou l’organisation mémoire.
    

---

```markdown
# 📘 Chapitre 2 – Partie 2  
## Organisation Physique des Données & Indexation dans les Bases de Données  

---

## 🌐 1️⃣ Notion d’Index

### 🧠 Principe général
```

```
  🔍 Requête : "Nom = 'Ali'"
              │
              ▼
```

┌─────────────┐  
│ Fichier │ (table principale)  
└─────────────┘  
▲  
│ adresse trouvée dans  
│  
┌─────────────┐  
│ Index │ (valeur → adresse)  
└─────────────┘

```

**Recherche en deux étapes :**
1️⃣ Trouver l’adresse dans le fichier d’index  
2️⃣ Accéder directement à l’enregistrement sur disque  

---

## 📂 2️⃣ Typologie des Index

### 🧩 Index Dense (كثيف)
```

Index Dense :  
[valeur → adresse]  
───────────────────────  
Ali → Bloc 1  
Aya → Bloc 2  
Nadir → Bloc 3  
Redha → Bloc 4

```

### 📦 Index Non-Dense (غير كثيف)
```

Index Non-Dense :  
[bloc → première valeur]  
──────────────────────────────  
Bloc 1 → Ali  
Bloc 2 → Mohamed  
Bloc 3 → Redha

```

🧠 Dense = plus précis  
📉 Non-dense = plus petit mais moins exact  

---

## 🌳 3️⃣ Arbres B et B+

### 🌿 Structure générale
```

```
      [40]
     /    \
```

[20] [60, 80]  
/ \ /  
[10][30] [50][70][90]

```

- **Racine** = nœud supérieur  
- **Feuilles** = nœuds du bas contenant les données réelles  

---

### 🌲 Arbre B+ (toutes les données dans les feuilles)
```

```
           [40, 70]
          /    |     \
 [10,20,30] [40,50,60] [70,80,90]
    │           │            │
 données→→→→→→→→→→→→ chaînées →
```

```

- Données uniquement dans les feuilles  
- Les feuilles sont **chaînées** pour une lecture séquentielle rapide  
- Temps de recherche ≈ `O(log n)`  

---

## 💥 4️⃣ Hachage (Hashing – التجزئة)

### ⚙️ Principe
```

clé ("Ali") ──► h("Ali") = 2 ──► Bloc 2

```

### 🧮 Exemple de table de hachage
```

+----------+-----------+  
| Clé | Adresse |  
+----------+-----------+  
| Ali | Bloc 2 |  
| Aya | Bloc 1 |  
| Nadir | Bloc 3 |  
+----------+-----------+

```

### 🧱 Collision (تصادم)
```

h("Ali") = 2  
h("Ahmed") = 2 ❌ même bloc  
→ Chaînage (Linked list)

Bloc 2 → [Ali] → [Ahmed]

```

---

## 💾 5️⃣ Hachage Statique / Dynamique / Extensible

```

Statique : blocs fixes  
──────────────  
|0|1|2|3| ← taille constante

Dynamique : double la table si saturation  
──────────────  
|0|1|2|3|4|5|6|7|

Extensible : duplique seulement le bloc plein  
──────────────  
|0|1|2|3|  
↑ bloc plein → dupliqué

```

---

## 🧩 6️⃣ Index Bitmap (فهرس بتّي)
```

Relation Personne  
───────────────  
|Nom | Sexe | Situation|  
────────────────────────  
|Ali | M | Marié |  
|Aya | F | Célibataire|

Index bitmap pour Sexe (M/F)  
───────────────  
Nom M F  
───────────────  
Ali 1 0  
Aya 0 1

````

🧠 Requête :
```sql
SELECT * FROM Personne
WHERE sexe='M' AND situation='Marié';
````

➡️ combine les bitmaps par **AND** logique

```
[M]   1 0
[Marié] 1 0
AND →   1 0  ✅ = Ali
```

---

## 🧮 7️⃣ Formules essentielles (ملخص القوانين)

|Concept|Formule|Traduction|
|---|---|---|
|Densité d’un Index|$$D = \frac{Nb_{clés}}{Nb_{enregistrements}}$$|كثافة الفهرس|
|Adresse relative (hachage)|$$AR = N \times L$$|العنوان النسبي|
|Hit Ratio (cache)|$$HR = \frac{Accès_{cache}}{Accès_{total}}$$|نسبة النجاح|
|Capacité bloc|$$N = \frac{B}{E}$$|عدد السجلات في كتلة|
|Recherche B/B+|`O(log n)`|التعقيد اللوغاريتمي|

---

✅ **Récapitulatif**

- Les **index** accélèrent la recherche
    
- Les **arbres B+** maintiennent un accès équilibré
    
- Le **hachage** permet un accès direct
    
- Les **bitmaps** servent aux filtres booléens
    
- Les **formules** aident à mesurer la performance et la capacité de stockage
    
