# 🎬 BD CINEMA – Script SQL & Accès Java (Corrigé type)

> ⚠️ **Hypothèses raisonnables (standard cinéma)**  
> Les tables suivantes existent déjà dans `scriptcinema.sql` :

- `individu(num_individu PK, ...)`
    
- `film(num_film PK, ...)`
    
- `cinema(num_cinema PK, ...)`
    
- `projection(num_film FK, num_cinema FK, date_projection, ...)`
    

Si les noms diffèrent légèrement, adaptez-les (la logique reste identique).

---

## 1️⃣ Création de la BD Cinema

```sql
CREATE DATABASE IF NOT EXISTS Cinema;
USE Cinema;

-- Ouvrir puis exécuter le fichier fourni par l'enseignant
-- SOURCE scriptcinema.sql;   -- (Workbench : File > Open SQL Script > Execute)
```

🔄 **Refresh** : clic droit sur _Schemas_ → Refresh

---

## 2️⃣ Table `regarder_film`

```sql
CREATE TABLE regarder_film (
    num_individu INT,
    num_film INT,
    num_cinema INT,
    date_acces DATE,
    PRIMARY KEY (num_individu, num_film, num_cinema, date_acces),
    FOREIGN KEY (num_individu) REFERENCES individu(num_individu),
    FOREIGN KEY (num_film) REFERENCES film(num_film),
    FOREIGN KEY (num_cinema) REFERENCES cinema(num_cinema)
);
```

📌 Cette table enregistre **qui a regardé quel film, où et quand**.

---

## 3️⃣ Procédure : insertion avec vérification de date

🎯 **Objectif** :

- Insérer dans `regarder_film`
    
- Vérifier que `date_acces = date_projection`
    
- Retourner un message de confirmation
    

```sql
DELIMITER $$

CREATE PROCEDURE inserer_regarder_film (
    IN p_num_individu INT,
    IN p_num_film INT,
    IN p_num_cinema INT,
    IN p_date_acces DATE
)
BEGIN
    DECLARE v_count INT;

    SELECT COUNT(*) INTO v_count
    FROM projection
    WHERE num_film = p_num_film
      AND num_cinema = p_num_cinema
      AND date_projection = p_date_acces;

    IF v_count > 0 THEN
        INSERT INTO regarder_film
        VALUES (p_num_individu, p_num_film, p_num_cinema, p_date_acces);

        SELECT '✅ Insertion effectuée avec succès' AS Message;
    ELSE
        SELECT '❌ Date invalide : aucune projection à cette date' AS Message;
    END IF;
END $$

DELIMITER ;
```

---

## 4️⃣ Table `Stats`

📊 **Statistiques mensuelles par film et cinéma**

```sql
CREATE TABLE Stats (
    num_film INT,
    num_cinema INT,
    date_stats DATE,
    NB_spectateurs INT,
    PRIMARY KEY (num_film, num_cinema, date_stats),
    FOREIGN KEY (num_film) REFERENCES film(num_film),
    FOREIGN KEY (num_cinema) REFERENCES cinema(num_cinema)
);
```

---

## 5️⃣ Procédure : remplissage de la table Stats

🎯 Calcule le nombre de spectateurs **par mois et par année**.

```sql
DELIMITER $$

CREATE PROCEDURE remplir_stats (
    IN p_date_stats DATE
)
BEGIN
    INSERT INTO Stats (num_film, num_cinema, date_stats, NB_spectateurs)
    SELECT
        num_film,
        num_cinema,
        p_date_stats,
        COUNT(*) AS NB_spectateurs
    FROM regarder_film
    WHERE MONTH(date_acces) = MONTH(p_date_stats)
      AND YEAR(date_acces) = YEAR(p_date_stats)
    GROUP BY num_film, num_cinema;
END $$

DELIMITER ;
```

---

## 6️⃣ Procédure : film le plus regardé du mois

🎯 Retourne **le numéro du film le plus regardé** pour un mois donné.

```sql
DELIMITER $$

CREATE PROCEDURE film_plus_regarde (
    IN p_date_F DATE
)
BEGIN
    SELECT num_film
    FROM regarder_film
    WHERE MONTH(date_acces) = MONTH(p_date_F)
      AND YEAR(date_acces) = YEAR(p_date_F)
    GROUP BY num_film
    ORDER BY COUNT(*) DESC
    LIMIT 1;
END $$

DELIMITER ;
```

---

# ☕ Accès à la BD en Java (JDBC)

## Connexion à MySQL

```java
import java.sql.*;

public class DBConnection {
    public static Connection getConnection() throws Exception {
        String url = "jdbc:mysql://localhost:3306/cinema";
        String user = "root";
        String password = "NewPassword123";

        return DriverManager.getConnection(url, user, password);
    }
}
```

---

## Appel de la procédure `inserer_regarder_film`

```java
import java.sql.*;

public class TestInsertion {
    public static void main(String[] args) throws Exception {
        Connection cn = DBConnection.getConnection();

        CallableStatement cs = cn.prepareCall(
            "{CALL inserer_regarder_film(?,?,?,?)}"
        );

        cs.setInt(1, 1);   // num_individu
        cs.setInt(2, 10);  // num_film
        cs.setInt(3, 2);   // num_cinema
        cs.setDate(4, Date.valueOf("2025-03-10"));

        ResultSet rs = cs.executeQuery();
        if (rs.next()) {
            System.out.println(rs.getString(1));
        }

        cn.close();
    }
}
```

---

## Appel de la procédure `film_plus_regarde`

```java
CallableStatement cs = cn.prepareCall(
    "{CALL film_plus_regarde(?)}"
);
cs.setDate(1, Date.valueOf("2025-03-01"));

ResultSet rs = cs.executeQuery();
if (rs.next()) {
    System.out.println("Film le plus regardé : " + rs.getInt(1));
}
```

---

## ✅ À remettre

✔ Script SQL complet (BD + tables + procédures)  
✔ Code Java JDBC d'accès à la BD

🎓 **Ce corrigé est prêt pour remise / examen / TP noté**

---
## 🔗 Navigation
- **Module:** [[NTIC L3/TABD/TABD|◀ TABD]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
