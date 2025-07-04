# 🗳️ Prédiction électorale par commune – MSPR TPRE813

Ce projet s’inscrit dans le cadre de la **Mise en Situation Professionnelle Reconstituée (MSPR)** du bloc de compétences *"Piloter l’informatique décisionnelle d’un SI (Big Data & BI)"*.  
L’objectif est de construire un **pipeline data complet**, permettant de **prédire l’orientation politique majoritaire** d’une commune à partir de données socio-économiques et territoriales publiques.

## 🏗️ Architecture technique

Ce projet repose sur une **infrastructure cloud entièrement hébergée sur Google Cloud Platform (GCP)**.  
Nous avons mis en place une architecture moderne en trois couches (Bronze → Silver → Gold) :

- **Bronze Layer** : Données brutes (CSV INSEE, élections, sécurité…) stockées dans un **bucket Google Cloud Storage (GCS)**.
- **Silver Layer** : Données nettoyées et normalisées, stockées dans un **entrepôt BigQuery**, modélisé selon un **schéma en étoile**.
- **Gold Layer** : Données agrégées et consolidées dans une **table unique**, prêtes pour la BI et la Data Science.

## 📦 Contenu du dépôt

- `notebooks/` : Notebooks **Python** utilisant **Pandas** pour le nettoyage et **Scikit-learn** pour la modélisation supervisée (Random Forest, etc.).  
  → Ces notebooks interagissent directement avec nos **tables BigQuery** et exploitent notre **bucket GCS** pour charger/exporter les données.

- `sqlx/` : Fichiers **SQLX (Dataform)** contenant les transformations SQL appliquées dans BigQuery pour passer de la couche Silver à la couche Gold.  
  → Chaque fichier correspond à un modèle (vue, table matérialisée...) orchestré via Dataform.

- `README.md` : Documentation du projet (ce fichier).

## 🤖 Machine Learning

Le modèle final retenu est un **Random Forest Classifier**, entraîné à partir de la table Gold consolidée.  
L’apprentissage supervisé est effectué via **Scikit-learn**, avec les données directement chargées depuis **BigQuery**.

Nous évaluons les performances à l’aide d’indicateurs standards (accuracy, f1-score, recall) et utilisons la **validation croisée** pour garantir la robustesse du modèle.

## 📊 Datavisualisation

Pour la restitution visuelle des données et des résultats, nous avons utilisé **Tableau Public**.  
Nos visualisations sont accessibles via le lien suivant :

🔗 [Scatter Plot: Propriétaires RP x Vote x Niveau de vie médian, sur Tableau Public](https://public.tableau.com/app/profile/agoat.delavega/viz/MSPR_DATA_VIZ_Agathe_Anthony_scatterplot/PropritairesRPxVotexNiveaudeviemdian)  
🔗 [World Map: Densité x Abstention sur Tableau Public](https://public.tableau.com/app/profile/agoat.delavega/viz/MSPR_DATA_VIZ_Agathe_Anthony/DensitxAbstention)  
🔗 [World Map: Vote à gauche x Chomage x Sans Diplomes, en Image](https://i.imgur.com/QDZc9Ei.png)  
🔗 [World Map: Vote au centre x Niveau de vie médian x Master/Doctorat, en Image](https://i.imgur.com/8n72sv1.png)  
🔗 [World Map: Vote à droite x Actifs Trajets Voiture (Ruralité), en Image](https://i.imgur.com/bK2vWWm.png)  


## ☁️ Prérequis et environnement

- Compte Google Cloud avec accès à :
  - un **bucket GCS** pour les fichiers bruts
  - un **projet GCP** avec un **dataset BigQuery** configuré
  - un **workspace Dataform** pour exécuter les modèles SQLX
- Python ≥ 3.9, avec les librairies : `pandas`, `google-cloud-bigquery`, `scikit-learn`, `matplotlib`, etc.

## 🧠 Auteurs

Projet réalisé par **Agathe A.T** et **Anthony J.** en **I1 2024/25 de l'EPSI Paris**  
Dans le cadre du module **TPRE813 – Big Data & Analyse de données** (Certification RNCP N°35584 – Expert en Informatique & SI)

---

