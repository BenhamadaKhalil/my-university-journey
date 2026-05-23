# 🧠 Chapitre 1 – Rappels sur les Bases de Données

## 🎯 Objectif du cours

Revoir les notions essentielles pour :

- Créer une **base de données relationnelle (قاعدة بيانات علائقية)**
    
- Manipuler les données avec **SQL (لغة الاستعلام المهيكلة)**
    

---

## 🧩 1. Définitions fondamentales (التعريفات الأساسية)

### 🗃️ Base de Données (BD)

> Ensemble **structuré (منظم)** de données représentant un **univers précis (مجال محدد)**, accessible à plusieurs utilisateurs **simultanément (في نفس الوقت)**

**Caractéristiques (الخصائص)** :

- 💾 Stockage permanent (تخزين دائم) de grandes quantités d’informations
    
- 👥 Accès multi-utilisateurs (وصول متعدد المستخدمين)
    
- 🔍 Facilite les opérations (يسهّل العمليات) : ajout، mise à jour، recherche
    

**Objectifs (الأهداف)** :

- 🚫 Éliminer la **redondance (التكرار)**
    
- 🔄 Assurer l’**indépendance (الاستقلالية)** entre programmes et données
    
- 🧱 **Intégrer (دمج)** toutes les données dans un espace commun
    

---

### 💻 Système de Gestion de Base de Données (SGBD = نظام إدارة قواعد البيانات)

> Logiciel (برنامج) qui gère la création، le stockage، la mise à jour (التحديث) et la consultation (الاستعلام) d’une BD

**Fonctions principales (الوظائف الرئيسية)** :

- 🧱 Structuration et stockage (تنظيم وتخزين) des données
    
- 🧠 Définition et manipulation (تعريف ومعالجة) des données :
    
    - **LDD (Langage de Définition des Données = لغة تعريف البيانات)**
        
    - **LMD (Langage de Manipulation des Données = لغة معالجة البيانات)**
        
- 🔒 Sécurité et confidentialité (الأمان والسرية)
    
- 🔁 Gestion des accès concurrents (إدارة الوصول المتزامن)
    
- 💡 Fiabilité (الموثوقية) et reprise après panne (الاسترجاع بعد الأعطال)
    

**Exemples (أمثلة)** :

- Bureautique (مكتبي) : `Access`, `Base`, `FileMaker`
    
- Serveurs (خوادم) : `Oracle`, `DB2`, `SQL Server`, `PostgreSQL`, `MySQL`
    

---

## 🧭 2. Niveaux de description des données (مستويات وصف البيانات)

|Niveau (المستوى)|Description (الوصف)|Représentation (التمثيل)|
|---|---|---|
|**Externe**|Vue utilisateur (منظور المستخدم)|Schéma externe (مخطط خارجي)|
|**Conceptuel**|Structure logique (الهيكل المنطقي) des données|Modèle Entité-Association (نموذج الكيان-العلاقة)|
|**Interne (Physique)**|Organisation réelle (التنظيم الفعلي) sur disque|Fichiers و index (ملفات وفهارس)|

💡 **Idée clé (فكرة أساسية)** :

> Chaque niveau simplifie (يبسّط) la compréhension et la maintenance des données.

---

## 🧱 3. Modèles de représentation (نماذج التمثيل)

|Modèle (النموذج)|Dépendances (الاعتماد)|Contenu (المحتوى)|
|---|---|---|
|**Conceptuel**|Indépendant du SGBD (مستقل عن النظام)|Entités و Associations (كيانات وعلاقات)|
|**Logique**|Dépend du modèle (يعتمد على النموذج)|Tables و Clés (جداول ومفاتيح)|
|**Physique**|Dépend du SGBD (يعتمد على النظام)|Types و Index (أنواع وفهارس)|

---

## 🧮 4. Étapes de conception d’une BD (مراحل تصميم قاعدة البيانات)

```mermaid
graph TD
A[Analyse du domaine réel (تحليل المجال الواقعي)] --> B[Modèle Conceptuel (النموذج المفاهيمي)]
B --> C[Modèle Logique (النموذج المنطقي)]
C --> D[Implémentation sur le SGBD (التنفيذ على نظام إدارة قاعدة البيانات)]
```

|Étape (المرحلة)|Niveau (المستوى)|Résultat (النتيجة)|
|---|---|---|
|Modélisation (النمذجة)|Conceptuel|Modèle E-A|
|Transformation (التحويل)|Logique|Modèle relationnel|
|Réalisation (التنفيذ)|Physique|Tables و fichiers SQL|

---

## 🧰 5. Modèle Conceptuel de Données (MCD = النموذج المفاهيمي للبيانات)

### 🧑‍💼 Entité (كيان)

Objet identifiable du monde réel (عنصر يمكن تمييزه من العالم الواقعي).

> Exemple : **Chauffeur**, **Voiture**, **Client**

Chaque entité a :

- Un **identifiant unique (معرّف فريد)**
    
- Des **attributs (خصائص)**
    

### 🔗 Association (علاقة)

Lien logique entre plusieurs entités (رابط منطقي بين كيانات متعددة).

> Exemple : _Chauffeur_ « utilise » _Voiture_.

### 📋 Exemple MCD

```
Chauffeur (NumCh, Nom, Prenom, Age, Adresse, Tel)
Voiture (Numvoit, Genre, Couleur)
utiliser (Date, Duree)
```

**Cardinalités (التعددية)** : Chauffeur (0,n) ↔ (0,n) Voiture

---

## 🧩 6. Modèle Logique de Données (MLD = النموذج المنطقي للبيانات)

> Traduction du MCD vers le modèle relationnel (ترجمة النموذج المفاهيمي إلى النموذج العلائقي)

Chaque **table (جدول)** contient :

- 🧭 **Clé primaire (المفتاح الأساسي – Primary Key)**
    
- 🔗 **Clé étrangère (المفتاح الأجنبي – Foreign Key)**
    
- 📋 **Attributs (خصائص / أعمدة)**
    

---

## 🔄 7. Passage du MCD vers le MLD (الانتقال من النموذج المفاهيمي إلى المنطقي)

### 1️⃣ Entité → Table

```
Entité : Chauffeur
↓
Table : Chauffeur(NumCh PK, Nom, Prenom, Age, Adresse, Tel)
```

### 2️⃣ Association 1 – N

> Le côté "N" contient une **clé étrangère** vers le côté "1".

```
Chauffeur (NumCh PK, Nom, Prenom, Age, Adresse, Tel)
Voiture (Numvoit PK, Genre, Couleur, Conducteur# FK)
```

### 3️⃣ Association N – N

> Créer une **nouvelle table d’association (جدول علاقة جديد)** avec les deux clés primaires.

```
utiliser (NumCh# FK, Numvoit# FK, Date, Duree)
```

→ Clé primaire = (NumCh#, Numvoit#)

### 4️⃣ Association 1 – 1

Deux options :

1. Fusionner (دمج) les deux entités.
    
2. Garder deux tables مع clé étrangère dans l’une.
    

---

## ⚙️ 8. Modèle Physique de Données (MPD = النموذج الفيزيائي للبيانات)

> Traduction concrète (ترجمة عملية) en SQL.

```sql
CREATE TABLE Chauffeur (
  NumCh INT PRIMARY KEY,
  Nom VARCHAR(20),
  Prenom VARCHAR(20),
  Age INT,
  Adresse VARCHAR(50),
  Tel VARCHAR(10)
);

CREATE TABLE Voiture (
  Numvoit INT PRIMARY KEY,
  Genre VARCHAR(20),
  Couleur VARCHAR(10),
  Conducteur INT,
  FOREIGN KEY (Conducteur) REFERENCES Chauffeur(NumCh)
);
```

---

## 🧾 9. Récapitulatif global (ملخص شامل)

|Niveau (المستوى)|Représentation (التمثيل)|Exemple (مثال)|
|---|---|---|
|**Conceptuel**|Entités & Associations|Chauffeur utilise Voiture|
|**Logique**|Tables & Clés|Chauffeur(NumCh), Voiture(Numvoit, Conducteur#)|
|**Physique**|SQL & Fichiers|CREATE TABLE Chauffeur …|

---

## 🧠 Points clés à retenir (نِقاط مهمة يجب تذكرها)

- Le **MCD** modélise le monde réel (يمثل العالم الواقعي).
    
- Le **MLD** le traduit en tables relationnelles (يحوله إلى جداول).
    
- Le **MPD** est l’implémentation réelle (SQL).
    
- Les **cardinalités (التعددية)** montrent les liens entre entités.
    
- Le **SGBD** assure la sécurité والتكامل (الأمان والتكامل).
    

---

## 🧩 Mini Quiz (اختبار صغير)

1. Quelle est la différence entre MCD et MLD ؟
    
2. Que devient une association N–N dans le modèle relationnel ؟
    
3. Pourquoi le SGBD est-il essentiel à la gestion des données ؟
    

---

---
## 🔗 Navigation
- **Module:** [[NTIC L3/TABD/TABD|◀ TABD]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
