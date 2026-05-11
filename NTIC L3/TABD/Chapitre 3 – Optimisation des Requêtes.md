# 📘 Chapitre 3 – Optimisation des Requêtes

## Partie 1 : Optimisation Syntaxique (avec exemples détaillés)

Source : Cours _Optimisation des Requêtes – Dr Bouanaka Chafia_

---

## 1️⃣ Pourquoi optimiser une requête ?

Une requête SQL :

- est **déclarative**
    
- ne précise **pas** :
    
    - l’ordre des opérations
        
    - les algorithmes utilisés
        
    - les chemins d’accès aux données
        

➡️ Le **SGBD** construit alors un **plan d’exécution**.

🎯 **Optimiser = choisir le plan qui coûte le moins cher**, en termes de :

- volume de données manipulées
    
- temps d’exécution
    

---

## 2️⃣ Exemple introductif (cours)

### 📂 Schéma relationnel

```text
etudiant(cid, nom)
cours(idcours, nom_cours)
inscrire(cid, idcours)
```

---

### 📝 Requête 1 : retrouver l’étudiant _Benali_

#### SQL

```sql
SELECT *
FROM etudiant
WHERE nom = 'Benali';
```

#### Algèbre relationnelle

```
σ nom = 'Benali' (etudiant)
```

💡 **Optimisation possible**

- utiliser un **index** sur `etudiant.nom`
    
- éviter un parcours séquentiel
    

---

### 📝 Requête 2 : étudiants avec `cid < 00112235`

#### Algèbre relationnelle

```
π nom (σ cid < 00112235 (etudiant))
```

💡 On applique :

1. restriction (σ) → réduit le nombre de tuples
    
2. projection (π) → réduit le nombre d’attributs
    

---

### 📝 Requête 3 : étudiants inscrits au cours "TABD"

#### SQL

```sql
SELECT nom
FROM etudiant, inscrire, cours
WHERE etudiant.cid = inscrire.cid
AND inscrire.idcours = cours.idcours
AND cours.nom_cours = 'TABD';
```

#### Expression algébrique naïve

```
π nom (
  σ nom_cours='TABD'
  (etudiant ⨝ inscrire ⨝ cours)
)
```

❌ **Problème** : jointures faites trop tôt → grandes tables intermédiaires

---

## 3️⃣ Principe fondamental de l’optimisation syntaxique

### 📌 Observation clé du cours

- **Opérateurs unaires (σ, π)** → tables plus petites
    
- **Opérateurs binaires (⨝, ×)** → tables plus grandes
    

👉 **Règle d’or** :

> Faire les restrictions et projections **avant** les jointures

---

## 4️⃣ Plan d’Exécution

### 🔹 Plan logique

- arbre d’opérateurs algébriques
    
- indépendant du SGBD
    

### 🔹 Plan physique

- plan logique + algorithmes réels :
    
    - index scan
        
    - hash join
        
    - nested loop join
        

---

## 5️⃣ Optimisation Syntaxique – Étapes détaillées

---

### ✳️ Étape 1 : Traduction SQL → Algèbre Relationnelle

#### Exemple du cours

```sql
SELECT Nom, Bureau
FROM Employe, Departement
WHERE Employe.numoD = Departement.numoD
AND Employe.salaire > 1000;
```

#### Traduction algébrique

```
π Nom, Bureau (
  σ Employe.salaire > 1000
  (Employe ⨝ Employe.numoD = Departement.numoD Departement)
)
```

---

### ✳️ Étape 2 : Arbre algébrique

- Feuilles : `Employe`, `Departement`
    
- Nœuds :
    
    - jointure
        
    - restriction
        
    - projection
        
- Racine : projection finale
    

---

### ✳️ Étape 3 : Application des règles de transformation

---

## 6️⃣ Règles de Transformation (avec exemples)

---

### 🔹 Règle 1 : Commutativité & associativité (⨝, ×)

```
E1 ⨝ E2 = E2 ⨝ E1
(E1 ⨝ E2) ⨝ E3 = E1 ⨝ (E2 ⨝ E3)
```

📌 **Utilité**

- changer l’ordre des jointures
    
- choisir l’ordre qui génère les plus petites tables
    

---

### 🔹 Règle 2 : Regroupement des projections

```
π A (π B (E)) = π A (E)
```

📌 **Exemple**

```text
π nom (π nom, salaire (Employe))
= π nom (Employe)
```

---

### 🔹 Règle 3 : Regroupement des restrictions

```
σ F1 (σ F2 (E)) = σ (F1 ∧ F2) (E)
```

📌 **Exemple**

```text
σ salaire>1000 (σ age>30 (Employe))
= σ salaire>1000 ∧ age>30 (Employe)
```

---

### 🔹 Règle 4 : Descente des restrictions

```
σ F (E1 ⨝ E2) = σ F (E1) ⨝ E2
(si F porte uniquement sur E1)
```

📌 **Exemple**

```text
σ salaire>1000 (Employe ⨝ Departement)
→ (σ salaire>1000 (Employe)) ⨝ Departement
```

✔️ réduit fortement les données avant la jointure

---

### 🔹 Règle 5 : Restriction ↔ Projection

```
π A (σ F (E)) = σ F (π A (E))
(si F utilise uniquement A)
```

---

### 🔹 Règle 6 : Descente des projections

```
π A (E1 ⨝ E2) =
π A (
  π A1 (E1) ⨝ π A2 (E2)
)
```

📌 Objectif :

- supprimer les colonnes inutiles **avant** la jointure
    

---

## 7️⃣ Algorithme d’Optimisation (cours)

1. Séparer les restrictions complexes (R3)
    
2. Descendre les restrictions au plus bas (R4, R5)
    
3. Regrouper les restrictions par relation
    
4. Séparer les projections (R2)
    
5. Descendre les projections (R6)
    
6. Regrouper les projections successives
    

---

## 8️⃣ Exemple final optimisé (idée générale)

### ❌ Plan non optimisé

```
π
 |
σ
 |
⨝
/ \
Employe  Departement
```

### ✅ Plan optimisé

```
π
 |
⨝
/ \
σ Employe   π Departement
```

✔️ moins de tuples  
✔️ moins d’attributs  
✔️ coût réduit

---

## 🧠 Résumé à mémoriser

> **L’optimisation syntaxique transforme une requête en expressions algébriques équivalentes afin de réduire les données intermédiaires avant l’exécution.**

---
