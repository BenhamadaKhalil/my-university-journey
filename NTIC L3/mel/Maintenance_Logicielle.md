 # 🛠️ Maintenance & Évolution Logicielle — Résumé Exam

> 💡 **Idée centrale** : La maintenance n'est pas une "réparation de bugs". C'est la **vie entière** d'un logiciel après livraison — et elle coûte **plus cher** que le développement initial.

---

## 📘 Chapitre 1 — Introduction à la Maintenance

### 🔖 Définitions (à citer en exam !)

| Source                 | Définition                                                                                                                                     |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **IEEE 610.12 (1993)** | Modification d'un logiciel *après livraison* pour corriger des défaillances, améliorer ses attributs ou l'adapter à un environnement changeant |
| **SWEBOK / ISO 14764** | **Totalité des activités** requises pour fournir un support coût-efficace — inclut des activités **avant** la livraison !                      |

> 🧠 **Différence clé** : IEEE = vision restrictive (post-livraison). SWEBOK = vision élargie (tout le cycle de vie, y compris la conception maintenable dès le début).

**Maintenance ≈ Évolution** : Lehman dit que c'est du "développement évolutif continu" sur un système préexistant. On préfère souvent dire "évolution" car "maintenance" évoque trop la simple réparation mécanique.

---

### 💸 Pourquoi c'est si coûteux ?

- 📊 La maintenance représente **60 à 90 %** du coût total de possession d'un logiciel
- ⚡ La **majorité** des coûts vient de l'évolution (perfective + adaptative), **pas des bugs**
- 🏗️ Un logiciel mal conçu au départ coûtera **beaucoup** plus cher à maintenir

**Exemple concret** 🏠 : c'est comme une maison. La construire coûte X€. Mais sur 30 ans, l'entretien, les rénovations, l'adaptation aux nouvelles normes... coûtent 2 à 4 fois plus !

---

### 😤 Les grandes difficultés

| Difficulté | Conséquence |
|-----------|------------|
| 🏗️ Mauvaise conception initiale (dette technique) | Chaque modif risque de tout casser |
| 📄 Documentation absente ou obsolète | On doit lire le code ligne par ligne |
| 🧩 Compréhension difficile | **40–60%** du temps de maintenance = juste comprendre le code |
| 👋 Turnover (départ des développeurs) | La connaissance implicite disparaît avec eux |
| 🌐 Environnement hétérogène | Tests de non-régression très complexes |

> 💡 **Astuce examen** : si on te demande pourquoi la maintenance est difficile → pense à ces 5 facteurs !

---

### ⚖️ Les Lois de Lehman *(très probables à l'exam)*

> Lehman a observé des centaines de logiciels depuis les années 1970. Ses lois décrivent pourquoi la maintenance est **inévitable**.

| Loi | Nom | Ce qu'elle dit | Exemple |
|-----|-----|----------------|---------|
| **I** | Changement continu | Un logiciel utilisé DOIT être adapté ou il devient progressivement inutile | Windows XP abandonné → incompatible avec le web moderne |
| **II** | Complexité croissante | Sans effort actif, chaque modif ajoute de la complexité | Ajouter des exceptions à la logique métier jusqu'à ce que plus personne ne comprenne rien |
| **III** | Stabilité organisationnelle | Le taux d'évolution reste relativement stable dans le temps | Une équipe ne peut absorber que X changements par mois |
| **IV** | Qualité déclinante | La qualité perçue baisse si on ne fait pas de maintenance active | Les utilisateurs trouvent le logiciel "de plus en plus lent et bugué" |

> 🎯 **Pour l'exam** : Loi I + Loi II sont les **plus importantes**. Loi II justifie directement la maintenance **préventive** et la **réingénierie**.

---

## 🔧 Chapitre 2 — Les 4 Types de Maintenance

> 🎯 **Méthode pour identifier le type** : pose-toi ces questions dans l'ordre :
> 1. Le logiciel est-il **cassé** ? → Corrective
> 2. L'**environnement** a changé ? → Adaptative
> 3. On veut l'**améliorer** ? → Perfective
> 4. On veut **prévenir** des pannes ? → Préventive

---

### ❌ 1. Maintenance Corrective

**Déclencheur** : quelque chose est cassé (bug, crash, faille sécurité)
**Nature** : **réactive** — on répare ce qui ne fonctionne plus
**Objectif** : rétablir le fonctionnement attendu

| Exemple concret | Détail |
|----------------|--------|
| 🔐 Patch injection SQL | Un attaquant peut accéder à la BDD via le champ de login → on corrige |
| 💾 Fuite mémoire | L'application ralentit après 2h d'utilisation → on cherche et corrige |
| 💰 Calcul TVA erroné | Le module financier calcule 19% au lieu de 20% → correction urgente |
| 🖥️ Crash sur Windows 11 | L'appli plante au démarrage sur le nouvel OS → fix |

> ⚠️ C'est ce que les gens associent le plus à "maintenance" — mais c'est souvent la **plus petite** partie du budget réel !

---

### 🔄 2. Maintenance Adaptative

**Déclencheur** : l'**environnement** a changé, mais le logiciel lui-même n'est pas "cassé"
**Nature** : réactive ou planifiée — maintenir la **compatibilité**
**Objectif** : que le logiciel continue à fonctionner dans son nouvel environnement

| Déclencheur | Exemple concret |
|------------|----------------|
| 🖥️ Nouveau système d'exploitation | Migration de Windows 7 vers Windows 11 → tester et corriger les incompatibilités |
| 🗄️ Mise à jour SGBD | MySQL 5.7 → MySQL 8.0 → certaines requêtes SQL ne fonctionnent plus |
| 📜 Nouvelle réglementation | RGPD 2018 → obligation d'ajouter le consentement cookies et le droit à l'oubli |
| 🔌 Changement d'API partenaire | L'API de paiement Stripe change de version → adapter les appels |
| ☁️ Migration cloud | Application on-premise → AWS → architecture à revoir |

> 💡 **Retenir** : le logiciel n'est pas cassé, c'est son **contexte** qui a changé.

---

### ✨ 3. Maintenance Perfective (= Évolutive)

**Déclencheur** : on veut rendre le logiciel **meilleur** ou **plus adapté aux besoins**
**Nature** : proactive ou réactive (suite à demande utilisateur)
**Objectif** : augmenter la valeur du logiciel

> 📊 C'est souvent la **plus grande part** des coûts de maintenance sur le long terme !

| Sous-type                  | Exemple concret                                                    |
| -------------------------- | ------------------------------------------------------------------ |
| ➕ Nouvelle fonctionnalité  | Ajouter l'export en PDF dans un rapport existant                   |
| ⚡ Optimisation performance | Une requête SQL met 10s → on l'optimise à 0.3s                     |
| 🎨 Amélioration UX         | Refonte de l'interface de connexion selon les standards actuels    |
| 🧹 Refactoring             | Diviser une fonction de 500 lignes en 10 fonctions compréhensibles |
| 🌍 Internationalisation    | Ajouter la langue arabe dans l'application                         |
| 🗑️ Suppression obsolète   | Retirer une fonctionnalité que 0% des utilisateurs utilisent       |

---

### 🛡️ 4. Maintenance Préventive

**Déclencheur** : audits, analyse statique, identification de risques futurs
**Nature** : **proactive** — agir avant que la panne arrive
**Objectif** : augmenter la robustesse, réduire les coûts futurs

| Exemple concret | Pourquoi c'est préventif |
|----------------|------------------------|
| 🔄 Mise à jour d'une librairie | Elle fonctionne encore, mais une faille sera découverte dans 6 mois |
| 📝 Améliorer la documentation | Personne ne comprend ce module → on documente avant que l'auteur parte |
| 🧪 Ajouter des tests unitaires | Le code "marche" mais sans tests, chaque modif est un risque |
| 🧹 Refactoring préventif | Module complexe identifié par analyse statique avant qu'il cause des bugs |

> ⚠️ La maintenance préventive est souvent **négligée** par manque de temps/budget — et c'est pour ça que la complexité augmente (Loi II de Lehman) !

---

### 📊 Tableau Récapitulatif

| Type           | Déclencheur            | Nature             | Priorité typique |
| -------------- | ---------------------- | ------------------ | ---------------- |
| ❌ Corrective   | Bug, crash, faille     | Réactive           | 🚨 Urgente       |
| 🔄 Adaptative  | Environnement change   | Réactive/planifiée | 📅 Planifiée     |
| ✨ Perfective   | Besoin d'évolution     | Proactive/réactive | 📈 Importante    |
| 🛡️ Préventive | Risque futur identifié | Proactive          | 🔮 Long terme    |

> 🎯 **Cas piège** : un patch de sécurité = ❌ Corrective (corrige une faille) ET 🛡️ Préventive (empêche exploitation future). L'important = identifier l'**intention principale** !

---

## 📏 Chapitre 3 — Les Métriques de Maintenance

> **Pourquoi mesurer ?** "On ne peut pas améliorer ce qu'on ne mesure pas." Les métriques transforment des impressions subjectives ("le code est complexe") en données objectives ("V(G) = 24").

---

### 🏗️ Métriques Produit (qualité du code)

#### LOC / SLOC — Lignes de Code
- **Ce que c'est** : simplement compter les lignes (physiques, logiques, ou non-vides)
- **Utilité** : normaliser d'autres métriques (ex: bugs par KLOC)
- ⚠️ **Piège** : 1000 lignes Java ≠ 1000 lignes Python ≠ 1000 lignes assembleur. LOC seul ne dit rien sur la complexité !

#### V(G) — Complexité Cyclomatique de McCabe ⭐

> **La métrique la plus importante à connaître pour l'exam !**

**Formule 1** (facile) : `V(G) = nombre de décisions + 1`
**Formule 2** (graphe) : `V(G) = E − N + 2P`
- E = arêtes du graphe de flot de contrôle
- N = nœuds
- P = composantes connexes (souvent = 1)

**Ce qu'on compte** : `if`, `else if`, `while`, `for`, `foreach`, `case`, `&&`, `||`, `?:`

```java
// Exemple de calcul V(G)
public String classify(int x, int y) {
    if (x > 0 && y > 0) {     // if = +1, && = +1
        return "deux positifs";
    } else if (x < 0) {        // else if = +1
        while (y-- > 0) {      // while = +1
            process();
        }
        return "x négatif";
    }
    return "autre";
}
// V(G) = 4 + 1 = 5
```

**Interprétation** :
- V(G) ≤ 10 → ✅ Simple, facile à tester
- 10 < V(G) ≤ 15 → ⚠️ Attention, complexité notable
- V(G) > 15 → 🚨 Complexe, difficile à tester, risque élevé de bugs

> 💡 V(G) indique aussi le **nombre minimum de cas de tests** pour couvrir tous les chemins !

#### Indice de Maintenabilité (MI)

**Formule** : combine V(G) moyen + LOC moyen + Volume Halstead (+ parfois taux commentaires)
**Échelle** : 0 à 100

| Score MI | Interprétation |
|---------|---------------|
| > 85 | ✅ Très maintenable |
| 65–85 | ⚠️ Maintenabilité moyenne |
| < 65 | 🚨 Difficile à maintenir |

#### Métriques Orientées Objet

| Métrique | Signification | Bon / Mauvais |
|---------|--------------|--------------|
| **DIT** (Depth of Inheritance Tree) | Profondeur d'héritage | Élevé = fragile |
| **CBO** (Coupling Between Objects) | Couplage entre classes | Élevé = 🚨 |
| **LCOM** (Lack of COhesion in Methods) | Manque de cohésion | Élevé = 🚨 |
| **NOC** (Number Of Children) | Nb de sous-classes | Élevé = impact fort |

> 🎯 Règle d'or OO : **couplage faible + cohésion forte** = code maintenable

---

### ⚡ Métriques Processus (efficacité de la maintenance)

#### MTTR — Mean Time To Repair
**Définition** : temps moyen entre la *détection* d'un bug et sa *résolution déployée en production*

**Exemple** : Bug détecté lundi 9h → analysé → corrigé → testé → déployé jeudi 14h = MTTR de ~77h

- MTTR faible = 🎉 équipe réactive, processus efficace
- MTTR élevé = 🚨 goulot quelque part (analyse ? tests ? déploiement ?)

#### Code Churn (Taux de Changement)
**Définition** : fréquence à laquelle les fichiers/modules sont modifiés

- Un module modifié toutes les semaines depuis 6 mois = 🚨 instabilité ou exigences floues
- Associer avec V(G) : module complexe + fort churn = **bombe à retardement**

#### Taux d'Échec des Changements
**Définition** : % de déploiements qui causent un incident en production

**Exemple** : 20 déploiements ce mois, 4 ont nécessité un rollback = 20% de taux d'échec → 🚨

---

### 🔗 Relation entre métriques produit et processus

```
V(G) élevé (produit)
    → Compréhension difficile
    → MTTR plus long (processus)
    → Plus de bugs réintroduits (processus)
    → Taux d'échec des changements plus élevé (processus)
```

> 💡 **Utilisation pratique** : identifier les modules avec V(G) > 15 ET fort churn → candidats prioritaires pour refactoring préventif !

---

## 🔮 Chapitre 4 — Prévision de la Maintenance

### 🎯 Pourquoi prévoir ?

- 💰 **Budgétisation** : allouer correctement les ressources
- 🧭 **Décision stratégique** : continuer / réingénieriser / remplacer ?
- ⚠️ **Gestion des risques** : anticiper les dépassements
- 📋 **Contrats SLA** : définir des niveaux de service réalistes

---

### 📐 Méthodes d'estimation de l'effort

#### Méthode du Pourcentage du Développement
```
Coût maintenance annuel ≈ 15% à 25% du coût de développement initial
```
**Exemple** : Application développée pour 200 000€ → maintenance ≈ 30 000 à 50 000€/an
- ✅ Très rapide à calculer
- ❌ Ignore la qualité du code, l'âge, la complexité réelle

#### COCOMO II (Constructive Cost Model)
Modèle paramétrique qui prend en compte :
- Taille (KSLOC = milliers de lignes)
- Complexité du produit
- Capacités de l'équipe
- Maturité des processus
- Niveau de réutilisation

- ✅ Plus précis, basé sur des facteurs réels
- ❌ Nécessite des données historiques pour calibrer

#### Benchmarking
Comparer avec des projets similaires déjà réalisés :
- ✅ Basé sur le réel
- ❌ Nécessite une base de données de projets comparables

#### Jugement d'Expert
- ✅ Prend en compte des facteurs qualitatifs
- ❌ Subjectif, dépend de la disponibilité des experts

> 💡 **En pratique** : on combine souvent 2–3 méthodes pour croiser les estimations.

---

### ⭐ Analyse d'Impact — Point Critique !

> **Définition** : processus consistant à identifier toutes les conséquences potentielles d'un changement proposé sur l'ensemble du système **avant** de l'approuver et de l'implémenter.

**Analogie** 🏥 : comme un chirurgien qui étudie les scanners avant d'opérer. On ne coupe pas sans savoir ce qu'il y a autour !

#### Objectifs de l'analyse d'impact

1. 🔍 Évaluer la **faisabilité technique** du changement
2. ⏱️ Estimer l'**effort et le coût** de la modification spécifique
3. 📋 Identifier tous les **éléments impactés** (code, doc, tests)
4. ⚠️ Détecter les **conflits** avec d'autres changements en cours
5. 🎲 Évaluer les **risques** (régression, performance, sécurité)
6. ✅ Prendre une décision éclairée **Go/No-Go**

#### Techniques

| Technique                      | Comment                                 | Exemple                                                             |
| ------------------------------ | --------------------------------------- | ------------------------------------------------------------------- |
| 🔗 **Analyse de dépendances**  | Graphes d'appels, héritage              | "Modifier cette classe impacte ces 7 autres classes"                |
| 🔄 **Traçabilité**             | Liens exigences ↔ code ↔ tests          | "Cette exigence est couverte par ces 3 tests"                       |
| 🔬 **Analyse statique**        | Outils d'analyse du code                | SonarQube détecte les dépendances                                   |
| 🧪 **Scénarios d'usage**       | Quels cas d'utilisation sont touchés ?  | "Les modules de facturation et de rapport utilisent cette fonction" |
| 👨‍💼 **Consultation experts** | Développeurs qui connaissent le système | "Le dev senior sait que ce module a un comportement non documenté"  |

#### Résultat de l'analyse d'impact
→ Un rapport contenant :
- Liste des éléments impactés
- Estimation affinée de l'effort
- Évaluation des risques
- **Recommandation Go/No-Go**

---

### 🔑 Facteurs influant sur les coûts

```
🏗️ Techniques          👥 Organisationnels      🌍 Environnementaux
────────────────────  ──────────────────────   ──────────────────
Complexité             Compétence équipe        Stabilité OS/DB
Qualité code           Turnover                 Nbre utilisateurs
Documentation          Processus définis        Pression marché
Âge (legacy)           Outils disponibles       Multi-plateformes
Technologie
```

---

## ⚙️ Chapitre 5 — Modèles de Processus d'Évolution

### 📋 Activités clés selon IEEE 14764 *(à savoir dans l'ordre !)*

```
1. 🏗️ Implémentation du processus
   └─ Plan de maintenance, procédures, outils, formation

2. 🔍 Analyse du problème
   └─ Réception RFC → classification → priorité → analyse d'impact → approbation

3. 🛠️ Implémentation de la modification
   └─ Conception → codage → tests unitaires → mise à jour documentation

4. ✅ Revue / Acceptation
   └─ Tests intégration → non-régression → UAT → approbation finale

5. 🚚 Migration
   └─ Déplacement vers nouvel environnement (si nécessaire)

6. 🗑️ Retrait
   └─ Fin de vie, archivage, notification utilisateurs
```

> ⚠️ **Exam** : l'analyse d'impact est dans l'étape 2 (Analyse du problème) !

---

### 🏃 Comparatif des modèles de processus

#### Cascade (Waterfall)
```
Analyse → Conception → Implémentation → Test → Déploiement
```
- ✅ Simple à gérer pour des corrections très bien définies
- ❌ Rigide, peu adapté à la nature imprévisible de la maintenance
- 🎯 **Idéal pour** : petites corrections isolées et bien comprises

#### Itératif/Incrémental
- Cycles courts avec livraisons fréquentes
- ✅ Plus flexible, mieux adapté à l'évolution continue
- 🎯 **Idéal pour** : maintenance évolutive planifiée

#### 🏃 Scrum (Agile)
```
Sprint Planning → Sprint (2-4 semaines) → Review → Rétrospective → ...
```
- Le Product Owner gère un **backlog** (liste priorisée bugs + améliorations)
- ✅ Très flexible, réactif, amélioration continue via rétrospectives
- ❌ Moins prédictif à long terme
- 🎯 **Idéal pour** : gestion d'un produit avec backlog mixte (bugs + features)

**Exemple concret** 🏃 : chaque sprint de 2 semaines, l'équipe prend les 5 items les plus urgents du backlog (2 bugs critiques, 3 petites améliorations), les réalise, livre, et recommence.

#### 📋 Kanban (Agile)
```
[To Do] → [In Progress] → [Testing] → [Done]
   WIP limite: 5     WIP limite: 3    WIP limite: 2
```
- Visualisation du flux + limitation du travail en cours (WIP)
- ✅ Idéal pour flux continu et imprévisible de tâches
- Pas de sprints fixes → les tâches avancent au fil de l'eau
- 🎯 **Idéal pour** : maintenance corrective continue (support L2/L3)

**Exemple concret** 📋 : un bug est signalé → va dans "To Do" → un dev le prend ("In Progress") → le teste → "Done". Pas besoin d'attendre la fin d'un sprint !

#### IEEE 14764
- Fournit les **activités fondamentales** intégrables dans n'importe quel modèle
- Pas un cycle de vie prescrit — c'est une **checklist** des activités essentielles
- 🎯 **Idéal pour** : tous types, sert de référence universelle

---

### 🚀 DevOps et Maintenance

> DevOps = Dev + Ops → fluidifier et automatiser la collaboration entre équipes

**Impact sur la maintenance :**
- **CI** (Intégration Continue) : chaque commit déclenche les tests automatiquement → détection rapide des régressions
- **CD** (Déploiement Continu) : les correctifs arrivent en production rapidement (heures/jours vs semaines)
- **Monitoring** continu : si une mise en prod cause un problème → l'équipe est alertée immédiatement
- **Infrastructure as Code** : l'environnement est versionné et reproductible

**Résultat** : la frontière entre développement et maintenance devient floue — c'est un flux continu d'évolution.

---

## 🔁 Chapitre 6 — Réingénierie de Systèmes Existants

### 🎯 Définition

> La réingénierie = analyser un système existant (legacy), le comprendre en profondeur, puis le **transformer et réimplémenter** dans une forme améliorée, tout en préservant ses fonctionnalités essentielles.

**Distinction importante :**
- **Restructuration** : améliore la structure interne sans changer l'architecture globale
- **Réingénierie** : inclut la restructuration + changement d'architecture possible + nouvelles technos
- **Forward Engineering** : développement classique depuis des spécifications

---

### 🧲 Modèle en Fer à Cheval *(à connaître pour l'exam !)*

```
┌─────────────────────────────────────────────────────┐
│  [Système existant]                                  │
│         │                                           │
│         ↓ ← Rétro-ingénierie (comprendre)           │
│  [Abstraction : conception, architecture, données]  │
│         │                                           │
│         ↓ ← Transformation (décider les changements)│
│  [Nouvelle conception / architecture]               │
│         │                                           │
│         ↓ ← Forward Engineering (reconstruire)      │
│  [Nouveau système amélioré]                         │
└─────────────────────────────────────────────────────┘
```

**Analogie** 🏚️→🏠 : c'est comme rénover une vieille maison. D'abord on inspecte tout (rétro-ingénierie), on décide ce qu'on garde/change (transformation), puis on reconstruit (forward engineering). On ne démolit pas tout !

---

### 🤔 Quand décider la réingénierie ?

| Signal d'alerte | Seuil de décision |
|----------------|------------------|
| 💸 Coûts de maintenance | Deviennent prohibitifs et continuent d'augmenter |
| 🚧 Blocage fonctionnel | Impossible d'ajouter des fonctionnalités critiques |
| 💀 Technologie obsolète | Non supportée, compétences introuvables sur le marché |
| ☁️ Migration stratégique | Besoin de passer au cloud ou aux microservices |
| 📉 Performance dégradée | SLA non respectés, impossible à optimiser |

---

### 🛠️ Techniques de réingénierie

| Technique             | Description                                       | Risque      | Quand utiliser                                    |
| --------------------- | ------------------------------------------------- | ----------- | ------------------------------------------------- |
| **Restructuration**   | Améliorer le code sans changer le comportement    | Faible      | Code lisible mais mal structuré                   |
| **Wrapping** 🎁       | Envelopper l'ancien système dans une nouvelle API | Très faible | Système stable mais interface obsolète            |
| **Migration données** | ETL vers nouveau schéma                           | Moyen       | Changement de SGBD                                |
| **Refactoring**       | Amélioration interne continue                     | Faible      | Réduction dette technique                         |
| **Remplacement COTS** | Remplacer par un composant commercial             | Variable    | Fonctionnalité générique disponible sur le marché |
| **Réécriture**        | Reconstruire from scratch                         | Élevé       | Legacy totalement inutilisable                    |

> 🎁 **Wrapping** : exemple concret — une vieille application COBOL mainframe qui calcule des pensions. Plutôt que de tout réécrire, on met une API REST devant elle. Les nouvelles applis appellent l'API, le COBOL tourne toujours en coulisses.

---

### 🧩 Réutilisation logicielle

**Pendant la maintenance** :
- Bibliothèques/frameworks standards (éviter de réinventer la roue)
- Réutiliser des modules internes existants

**Objectif de la réingénierie** :
- Extraire des composants en **services réutilisables** (ex: microservices)
- Rendre les modules indépendants → facilite leur réutilisation dans d'autres projets

**Remplacement par COTS** : si une bibliothèque open source fait déjà ce que fait un module legacy → remplacer !

---

## 🔍 Chapitre 7 — Rétro-ingénierie et Compréhension

### 😰 Le défi de la compréhension

> **Chiffre clé** : 40 à 60% de l'effort total de maintenance est consacré à la **compréhension** du code avant de pouvoir le modifier !

**Pourquoi c'est si difficile ?**

| Cause | Exemple concret |
|-------|----------------|
| 📚 Doc absente/obsolète | Le code dit `calculate()` mais la doc dit que ça fait autre chose |
| 👋 Turnover | Le dev qui a codé ce module est parti il y a 3 ans |
| 🏗️ Structure dégradée | 5 ans de "quick fixes" ont rendu le code incompréhensible |
| 💾 Code legacy | Application en COBOL des années 80, personne ne maîtrise plus |
| 🌐 Millions de lignes | Impossible d'avoir une vision globale |

---

### 🔎 Définition de la Rétro-ingénierie

> Analyser un système logiciel existant pour **identifier ses composants et leurs relations**, et créer des représentations à des **niveaux d'abstraction plus élevés** que le code source.

**Point clé** ⚠️ : la rétro-ingénierie **ne modifie pas** le système ! Elle produit de la **connaissance** sur le système.

**Différence avec réingénierie** :
- Rétro-ingénierie = **comprendre** (lecture seule)
- Réingénierie = **comprendre + transformer** (la rétro-ingénierie est la 1ère étape de la réingénierie)

---

### 🛠️ Techniques de rétro-ingénierie

#### Analyse Statique (sans exécuter le code)
- Lire le code source, identifier les dépendances
- Outils : analyseurs de code, générateurs de graphes d'appels
- **Résultats** : qui appelle qui, quelles classes dépendent de quelles autres

#### Analyse Dynamique (en exécutant le code)
- Profiling, traces d'exécution, débogage
- **Résultats** : comportement réel du programme, quelles fonctions sont appelées avec quelles données

#### Reconstruction de Modèles
- Générer des diagrammes UML à partir du code (classes, séquences, états)
- Reconstruire les modèles de données (schémas BDD)

---

### 🧠 Objectifs de la rétro-ingénierie

1. 💡 **Faciliter la compréhension** — fournir des vues abstraites pour naviguer dans le code
2. 📐 **Récupérer la conception perdue** — reconstituer l'architecture non documentée
3. 🔍 **Support à l'analyse d'impact** — identifier les dépendances avant une modification

---

## 🗂️ Chapitre 8 — Outils de Gestion de Configuration (SCM)

### 🔑 Principes fondamentaux du SCM

**SCM = Software Configuration Management** = gérer l'évolution de tous les artefacts logiciels

**3 activités clés :**

| Activité | Ce que ça fait | Exemple |
|---------|----------------|---------|
| **Identification** | Définir quoi gérer et comment les identifier | v1.2.3, branch-hotfix-login |
| **Contrôle** | Processus d'approbation des changements | Revue de code obligatoire avant merge |
| **Audit** | Traçabilité complète des modifications | Qui a changé quoi, quand, pourquoi |

---

### 🗃️ WinCVS — Gestion de versions

> CVS = Concurrent Versions System — un des premiers systèmes de contrôle de version

**Concepts clés :**

```
Repository (serveur)
    ↕
Checkout (copie locale) → Modifier → Commit (sauvegarder)
    ↕
Branche (travailler en parallèle) → Merge (réintégrer)
```

**Workflow typique** :
1. `checkout` → récupérer la dernière version
2. Modifier les fichiers localement
3. `commit` → envoyer les modifications au dépôt avec un message
4. Si conflit → résoudre manuellement + commit

**Utilité pour la maintenance** : pouvoir revenir en arrière si une modification casse quelque chose !

---

### 🐛 Bugzilla — Suivi de bugs

**Workflow d'un bug** :

```
NOUVEAU → ASSIGNÉ → EN COURS → RÉSOLU → VÉRIFIÉ → FERMÉ
                                    ↘ ROUVERT (si pas vraiment corrigé)
```

**Champs importants** :
- **Sévérité** : Blocker, Critical, Major, Normal, Minor, Trivial
- **Priorité** : P1 (urgent) à P5 (un jour peut-être)
- **Assigné à** : quel développeur traite ce bug
- **Version** : dans quelle version le bug a été trouvé / corrigé

**Valeur pour la maintenance** :
- Traçabilité : chaque correction est liée à un rapport de bug
- Historique : on peut voir quels modules génèrent le plus de bugs (→ cibles pour refactoring)
- Métriques : temps moyen de résolution, nombre de bugs par version (→ MTTR !)

---

## 🎯 Récap Express — Tout pour l'Exam

### ⚡ Identifier le type de maintenance (5 secondes)

```
Le logiciel plante / produit des résultats erronés ?        → ❌ Corrective
L'environnement a changé (OS, loi, API partenaire) ?       → 🔄 Adaptative
On ajoute / améliore une fonctionnalité ?                  → ✨ Perfective
On refactore / met à jour une lib encore fonctionnelle ?   → 🛡️ Préventive
```

### 📐 Formules à savoir

```
V(G) = nombre de décisions (if, while, for, case, &&, ||) + 1
V(G) = E - N + 2P  (formule graphe)

MI > 85  → ✅ très maintenable
MI 65-85 → ⚠️ moyen
MI < 65  → 🚨 problème

Coût maintenance ≈ 15-25% du coût développement / an (méthode simple)
```

### 🧲 Modèle en Fer à Cheval

```
Rétro-ingénierie (comprendre) → Transformation (décider) → Forward Engineering (reconstruire)
```

### 🏆 IEEE 14764 — Activités dans l'ordre

```
1. Implémentation processus
2. Analyse du problème + analyse d'impact ← point clé
3. Implémentation modification
4. Revue / Acceptation + tests non-régression
5. Migration (si applicable)
6. Retrait (fin de vie)
```

### ⚖️ Lois de Lehman

```
Loi I  → Changement continu inévitable (logiciel doit évoluer ou mourir)
Loi II → Complexité croissante sans effort actif (justifie prévention + réingénierie)
```

### 🔍 Analyse d'Impact = OBLIGATOIRE avant toute modification

```
Input  : Demande de changement (RFC)
Process: Dépendances + traçabilité + analyse statique + experts
Output : Rapport Go/No-Go + effort estimé + risques identifiés
```

### 📊 Répartition typique de l'effort de maintenance

```
✨ Perfective  ~50%   (nouvelles fonctionnalités, optimisations)
🔄 Adaptative  ~25%   (changements environnement)
❌ Corrective  ~20%   (bugs)
🛡️ Préventive  ~5%    (souvent négligée!)
```

> 💡 Ces chiffres varient selon les sources, mais l'ordre reste le même !

---

*📝 Bon courage pour l'exam ! L'essentiel : maîtriser les 4 types, savoir calculer V(G), comprendre l'analyse d'impact, et connaître les 2 premières lois de Lehman.*
