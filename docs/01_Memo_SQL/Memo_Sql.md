Voici un **résumé** des requêtes essentielles à maîtriserde en SQL :

---

### **1. Définitions**
- **SQL** (Structured Query Language) : Langage pour gérer et interroger des bases de données relationnelles.
- **SGBD** (Système de Gestion de Bases de Données) : Logiciel comme MySQL, PostgreSQL, Oracle, etc.

---

### **2. Les commandes fondamentales**
- **`SELECT`** : Lire des données  
  ```sql
  SELECT colonne1, colonne2 FROM table WHERE condition;
  ```
  Exemple :  
  ```sql
  SELECT nom, age FROM clients WHERE ville = 'Paris';
  ```

- **`INSERT`** : Ajouter des données  
  ```sql
  INSERT INTO table (colonne1, colonne2) VALUES (valeur1, valeur2);
  ```
  Exemple :  
  ```sql
  INSERT INTO clients (nom, age) VALUES ('Jean', 30);
  ```

- **`UPDATE`** : Modifier des données  
  ```sql
  UPDATE table SET colonne = nouvelle_valeur WHERE condition;
  ```
  Exemple :  
  ```sql
  UPDATE clients SET age = 31 WHERE nom = 'Jean';
  ```

- **`DELETE`** : Supprimer des données  
  ```sql
  DELETE FROM table WHERE condition;
  ```
  Exemple :  
  ```sql
  DELETE FROM clients WHERE age < 18;
  ```

---

### **3. Clauses importantes**
- **`WHERE`** : Filtre les résultats.  
  ```sql
  SELECT * FROM produits WHERE prix > 100;
  ```
- **`ORDER BY`** : Trier les résultats.  
  ```sql
  SELECT * FROM clients ORDER BY nom ASC;  -- ASC (croissant) ou DESC (décroissant)
  ```
- **`GROUP BY`** : Grouper pour des calculs (avec `COUNT`, `SUM`, `AVG`, etc.).  
  ```sql
  SELECT ville, COUNT(*) FROM clients GROUP BY ville;
  ```
- **`HAVING`** : Filtre sur les groupes (après `GROUP BY`).  
  ```sql
  SELECT ville, COUNT(*) FROM clients GROUP BY ville HAVING COUNT(*) > 5;
  ```

---

### **4. Jointure (JOIN)**
- **`JOIN`** : Récupère les données communes entre 2 tables.  
  ```sql
  SELECT table1.colonne, table2.colonne
  FROM table1
  JOIN table2 ON table1.id = table2.table1_id;
  ```
  *Exemple* :  
  ```sql
  SELECT commandes.id, clients.nom
  FROM commandes
  JOIN clients ON commandes.client_id = clients.id;
  ```
- **Éviter les ambiguïtés** : Si 2 tables ont une colonne du même nom, précise la table :  
  ```sql
  SELECT clients.nom, commandes.date  -- Mieux que juste "nom" ou "date"
  FROM clients
  JOIN commandes ON clients.id = commandes.client_id;
  ```
- **Jointures multiples** :  
  ```sql
  SELECT produits.nom, commandes.date, clients.nom
  FROM produits
  JOIN commandes ON produits.id = commandes.produit_id
  JOIN clients ON commandes.client_id = clients.id;
  ```
---

### **Exemple complet avec `JOIN`**  
```sql
-- Trouver les commandes passées par des clients de Paris, triées par date
SELECT clients.nom, commandes.date, commandes.montant
FROM clients
JOIN commandes ON clients.id = commandes.client_id
WHERE clients.ville = 'Paris'
ORDER BY commandes.date DESC;
```

---

### **5. Schéma de base de données**
- **Clé primaire (PRIMARY KEY)** : Identifiant unique (ex: `id`).  
- **Clé étrangère (FOREIGN KEY)** : Lien entre tables.  

Exemple de création de table :  
```sql
CREATE TABLE clients (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(50) NOT NULL,
    age INT,
    ville VARCHAR(50)
);
```

---

### **À retenir**
- Maîtriser les **requêtes `SELECT`** (avec `WHERE`, `ORDER BY`, `GROUP BY`).
- Savoir écrire des **`INSERT`/`UPDATE`/`DELETE`** simples.
- Comprendre les **jointures** (`JOIN`).
- Connaître les **opérateurs** (`=`, `>`, `LIKE`, `AND`, `OR`).

---

