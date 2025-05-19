##Projet : **Segmentation RFM Client via SQL sur BigQuery**

---

### Situation

L’entreprise souhaite mieux comprendre la valeur de ses clients afin de cibler ses campagnes marketing avec plus d’efficacité.
Le contexte est celui d’un retailer en ligne (dataset `thelook_ecommerce`) utilisant des données transactionnelles sur les 4 derniers mois.

---

###  Task

Créer une **segmentation RFM métier** :

* Analyser le comportement des clients en termes de récence, fréquence et montant d’achat
* Catégoriser les clients en 5 statuts (Platine, Gold, Silver, Bronze, Iron)
* Identifier les leviers CRM par segment via des KPI business (CA, volume, panier)

---

###  Actions

*  **Agrégation SQL** : j’ai utilisé `GROUP BY`, `DATE_DIFF()` et des filtres temporels pour isoler les clients actifs sur les 4 derniers mois.
*  **Calcul des quartiles** via `PERCENTILE_CONT()` pour découper la population selon la **valeur réelle**, et non pas par rang.
* **Scoring RFM** : chaque client a reçu un score de 1 à 4 sur **Récence**, **Fréquence**, et **Montant d’achat**, combiné ensuite pour créer un **score total RFM**.
*  **Attribution d’un statut client** selon des seuils métier :

  * `>= 10` → Platine
  * `>= 8` → Gold
  * `>= 6` → Silver
*  **Analyse finale** du CA par segment, du volume de clients, et du panier moyen

---

### 🟣 Results

| Segment | % Clients | CA total (€) | Fréquence moy. | Panier moyen (€) | Reco CRM                              |
| ------- | --------- | ------------ | -------------- | ---------------- | ------------------------------------- |
| Platine | 16 %      | 215 543 €    | 2,96           | 202 €            | Fidélisation haut de gamme            |
| Gold    | 21 %      | 200 889 €    | 1,91           | 141 €            | Engagement prioritaire                |
| Silver  | 30 %      | 144 117 €    | 1,15           | 72 €             | Potentiel de croissance               |
| Bronze  | 25 %      | 62 235 €     | 1,00           | 38 €             | Activation par promo                  |
| Iron    | 7 %       | 8 461 €      | 1,19           | 19 €             | À exclure ou réactiver ponctuellement |

---

#### 🎯 Insights business :

* **48 %** du chiffre d’affaires est généré par les **clients Platine + Gold** (seulement 38 % des clients)
* Le segment **Silver**, bien que majoritaire, est **sous-exploité en valeur**
* Le segment **Iron** représente un **coût inutile en activation marketing**

---

### 📤 Livrables

* 🧠 SQL complet exécuté sur BigQuery (RFM scoring + statuts + CA par segment)
* 📊 Tableau final interprétable par l’équipe marketing
* 📈 Recommandations activables CRM par statut



