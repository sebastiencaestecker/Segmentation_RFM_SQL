## 🧠 Projet : **Segmentation RFM Client via SQL sur BigQuery**

---

### 🟢 Situation

L’entreprise souhaite mieux comprendre la valeur de ses clients afin de cibler ses campagnes marketing avec plus d’efficacité.
Le contexte est celui d’un retailer en ligne (dataset `thelook_ecommerce`) utilisant des données transactionnelles sur les 4 derniers mois.

---

### 🟡 Task

Créer une **segmentation RFM métier** :

* Analyser le comportement des clients en termes de récence, fréquence et montant d’achat
* Catégoriser les clients en 5 statuts (Platine, Gold, Silver, Bronze, Iron)
* Identifier les leviers CRM par segment via des KPI business (CA, volume, panier)

---

### 🔵 Actions

#### 🔹 1. **Préparation des données sous BigQuery SQL**

* Agrégation des commandes : `recency`, `frequency`, `monetary`
* Périmètre : clients actifs sur les 4 derniers mois

#### 🔹 2. **Découpage intelligent via `PERCENTILE_CONT()`**

* Découpage des variables R/F/M en **quartiles réels** (`qcut` logique)
* Attribution de **scores de 1 à 4** pour chaque dimension
* Utilisation de `CROSS JOIN` pour appliquer les seuils à chaque client

#### 🔹 3. **Attribution d’un score RFM global + statut CRM**

```sql
CASE
  WHEN r_score + f_score + m_score >= 10 THEN 'Platine'
  WHEN ... THEN 'Gold' ...
```

#### 🔹 4. **Analyse des segments clients**

* Regroupement par statut
* Calcul du chiffre d’affaires par segment
* Part de clients et panier moyen via SQL analytique

---

### 🟣 Results

| Segment | CA total  | % clients | Fréquence moy. | Panier moyen |
| ------- | --------- | --------- | -------------- | ------------ |
| Platine | 215 543 € | 16 %      | 2,96           | 202,58 €     |
| Gold    | 200 889 € | 22 %      | 1,91           | 141,17 €     |
| Silver  | 144 117 € | 30 %      | 1,15           | 72,34 €      |
| Bronze  | 62 235 €  | 25 %      | 1,00           | 38,01 €      |
| Iron    | 8 461 €   | 7 %       | 1,19           | 19,06 €      |

#### 🎯 Insights business :

* **48 %** du chiffre d’affaires est généré par les **clients Platine + Gold** (seulement 38 % des clients)
* Le segment **Silver**, bien que majoritaire, est **sous-exploité en valeur**
* Le segment **Iron** représente un **coût inutile en activation marketing**

---

### 📤 Livrables

* 🧠 SQL complet exécuté sur BigQuery (RFM scoring + statuts + CA par segment)
* 📊 Tableau final interprétable par l’équipe marketing
* 📈 Recommandations activables CRM par statut


