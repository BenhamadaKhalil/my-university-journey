# 📘 Chapitre 3 – Optimisation des Requêtes

## Partie 2 : Optimisation Physique (avec exemples)

Source : _Optimisation des Requêtes – Partie 2_, Dr Bouanaka Chafia

---

## 1️⃣ Qu’est-ce que l’optimisation physique ?

### 🔹 Principe

L’optimisation physique intervient **après l’optimisation syntaxique**.

Elle prend en compte :

- les **index**
    
- les **statistiques** (taille des tables, sélectivité)
    
- la **mémoire tampon**
    
- les **algorithmes d’accès et de jointure**
    

🎯 **Objectif**

> Construire le **plan d’exécution physique (PEP)** le moins coûteux

---

## 2️⃣ Plan d’Exécution Physique (PEP)

### 🔹 Définition

Un **plan d’exécution physique** est :

- un **arbre d’opérateurs physiques**
    
- issus du **catalogue du SGBD**
    
- échangeant des **flux de tuples**
    

Les opérateurs :

- sont implémentés sous forme **d’itérateurs**
    
- peuvent être **bloquants** ou **non bloquants**
    

---

## 3️⃣ Modèle Itérateur (open / next / close)

Chaque opérateur implémente :

```text
open()  → initialisation
next()  → produire le prochain tuple
close() → libération des ressources
```

📌 **Pipeline**

- un opérateur consomme les tuples produits par un autre
    
- permet une exécution fluide
    

---

## 4️⃣ Modes d’exécution des opérateurs

### 🔸 Mode Matérialisation

- l’opérateur calcule **tout le résultat**
    
- stocke le résultat intermédiaire
    

❌ Inconvénients :

- forte consommation mémoire
    
- latence élevée
    

📌 Exemple :

```sql
SELECT MAX(salaire) FROM Employe;
```

➡️ tous les tuples doivent être lus avant de produire un résultat

---

### 🔸 Mode Pipeline

- le résultat est produit **à la demande**
    
- pas de stockage intermédiaire
    

✅ Avantages :

- faible latence
    
- moins de mémoire
    

📌 Exemple :

```sql
SELECT nom FROM Employe WHERE salaire > 1000;
```

---

## 5️⃣ Opérateurs Bloquants (important examen)

Un opérateur est **bloquant** s’il doit produire **tout son résultat** avant de continuer.

### Exemples bloquants :

- `SORT` (ORDER BY)
    
- `GROUP BY`
    
- `DISTINCT`
    
- `SUM`, `AVG`, `MIN`, `MAX`
    

➡️ **Pas de pipeline possible**

---

## 6️⃣ Types d’Opérateurs Physiques

---

### 🔹 1. Opérateurs d’accès

#### 🔸 FullScan (Parcours séquentiel)

- lit la table **bloc par bloc**
    
- très simple
    
- efficace si la table est petite ou si beaucoup de tuples sont sélectionnés
    

📌 Exemple :

```sql
SELECT * FROM Film;
```

**Bilan :**

- faible mémoire (1 bloc)
    
- temps de réponse court pour les premiers tuples
    

---

#### 🔸 IndexScan (Parcours par index)

- utilisé si un **index existe**
    
- accès direct aux valeurs recherchées
    

📌 Exemple :

```sql
SELECT * FROM Film WHERE annee = 2014;
```

➡️ Index sur `annee`

**Bilan :**

- très efficace
    
- peu de lectures disque
    

---

#### 🔸 DirectAccess (Accès par adresse)

- utilisé après un IndexScan
    
- accès direct au tuple via son adresse
    

📌 Chaîne typique :

```
IndexScan → DirectAccess → Table
```

---

### 🔹 2. Opérateurs de manipulation

- `Filter` (restriction)
    
- `Project` (projection)
    
- `Sort`
    
- `Join`
    
- `Merge`
    

---

## 7️⃣ Exemples de Plans d’Exécution (1 table)

---

### 🟢 Plan 1 : Sans index

```sql
SELECT titre
FROM Film
WHERE genre = 'SF' AND annee = 2014;
```

**Plan physique**

```
FullScan → Filter(genre, annee)
```

❌ Coûteux si la table est grande

---

### 🟢 Plan 2 : Avec index sur `annee`

```
IndexScan(annee=2014)
→ DirectAccess
→ Filter(genre='SF')
```

✅ Beaucoup moins de tuples testés  
✅ Coût réduit

---

## 8️⃣ Sélectivité (clé de décision)

### 🔹 Définition

La **sélectivité** mesure :

```
nombre de valeurs distinctes / nombre total de tuples
```

📌 Plus la sélectivité est élevée → plus l’index est utile

---

## 9️⃣ Algorithmes de Jointure (très important)

---

## 🔹 1. Nested Loop Join (sans index)

### Principe

Pour chaque tuple de R :

- comparer avec **tous** les tuples de S
    

```text
for r in R:
  for s in S:
    if r.A = s.A → produire (r,s)
```

❌ Très coûteux

### Coût

```
Coût = TR + TR × TS
```

📌 R = table externe (la plus petite)

---

## 🔹 2. Block Nested Loop Join

- lit des **blocs** au lieu des tuples
    
- réduit le nombre d’E/S disque
    

### Coût (mémoire M blocs)

```
Coût = TR + (TR / (M-1)) × TS
```

✅ Meilleur que Nested Loop simple

---

## 🔹 3. Jointure avec Index (Indexed Nested Loop)

### Principe

- parcourir R
    
- utiliser l’index sur S
    

📌 Exemple :

```sql
SELECT *
FROM Employe e, Departement d
WHERE e.numod = d.numod;
```

➡️ Index sur `Departement.numod`

### Coût

```
Scan(R) + accès index(S)
```

✅ Très efficace si l’index existe

---

## 🔹 4. Jointure par Tri-Fusion (Sort-Merge Join)

### Principe

1. Trier R et S sur l’attribut de jointure
    
2. Fusionner les deux relations
    

📌 Utilisée quand :

- pas d’index
    
- tables de grande taille
    

❌ Coût du tri  
✅ Bonne performance globale

---

## 🔹 5. Jointure par Hachage (Hash Join)

_(mentionnée dans le plan du cours)_

- créer une table de hachage sur la plus petite relation
    
- parcourir l’autre relation
    

✅ Très efficace  
❌ nécessite mémoire suffisante

---

## 🔟 Résumé Comparatif (examen)

|Algorithme|Index requis|Coût|Usage|
|---|---|---|---|
|Nested Loop|❌|Très élevé|Petites tables|
|Block Nested Loop|❌|Moyen|Mémoire limitée|
|Indexed Nested Loop|✅|Faible|Index disponible|
|Sort-Merge|❌|Moyen|Grandes tables|
|Hash Join|❌|Faible|Mémoire suffisante|

---

## 🧠 Résumé à mémoriser

> **L’optimisation physique choisit les opérateurs et algorithmes concrets (scan, index, jointure) afin de minimiser les E/S disque et le temps d’exécution.**

---
