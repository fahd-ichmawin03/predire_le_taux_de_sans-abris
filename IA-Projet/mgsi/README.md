# Prédiction du Taux de Sans-Abrisme en Californie

Ce projet, réalisé dans le cadre du module **Intelligence Artificielle / Machine Learning** à l'**ENSA Khouribga**, propose une approche basée sur la science des données pour estimer le taux de sans-abrisme (*homelessness*) en Californie. L'objectif est de fournir un outil prédictif capable d'identifier les zones géographiques vulnérables à partir de leurs caractéristiques démographiques et socio-économiques.

---

## Aperçu du Projet

* **Problématique :** Déterminer s'il est possible de prédire le sans-abrisme uniquement via des données démographiques pour remplacer les recensements manuels coûteux.
* **Données :** Jeu de données réel comprenant 130 zones d'apprentissage et 56 zones de test.
* **Variable Cible :** `HOMELESS_RATE`, présentant une distribution asymétrique à droite (*right-skewed*) nécessitant une transformation logarithmique pour stabiliser la variance.

---

## Méthodologie Technique

### 1. Ingénierie des Fonctionnalités (Feature Engineering)
Pour enrichir le modèle, plusieurs variables synthétiques ont été créées:
* **Groupes d'âge :** `JEUNES_PCT` (18-34 ans), `ACTIFS_PCT` (35-59 ans) et `SENIORS_PCT` (65+ ans).
* **Isolement Social :** `Single_PCT` (personnes vivant seules) et `social_isolation`.
* **Diversité :** `NON_WHITE_PCT` pour capturer les disparités ethniques.

### 2. Sélection de Variables
Nous avons appliqué la méthode **Recursive Feature Elimination (RFE)** pour réduire la dimensionnalité et éviter le sur-apprentissage (*overfitting*). Cette étape a permis de conserver une **"Whitelist" de 15 variables** critiques.

---

## Modélisation et Résultats

Trois approches principales ont été comparées pour identifier le modèle le plus robuste:

| Modèle | Meilleur Alpha | Val RMSE | Val $R^2$ |
| :--- | :--- | :--- | :--- |
| **Ridge Regression** | **1000** | **0.0030** | **-0.14** |
| Lasso Regression | 0.01 | 0.0033 | -0.38 |
| Random Forest | N/A | 0.0036 | 0.7095 |

> **Note :** Le modèle **Ridge** a été retenu comme référence (*Baseline*) finale en raison de sa capacité à stabiliser les coefficients sur un petit échantillon de données.

### Facteurs Clés de Prédiction (Importance Relative)
Selon l'analyse du modèle Random Forest, les leviers principaux sont:
1.  **AGE_25_34_PCT :** Le facteur le plus déterminant.
2.  **FAMILY_HH_TOTAL :** Souligne l'importance de la structure familiale.
3.  **DISABILITY_POP_PCT :** Signal fort lié à la vulnérabilité physique.

---

## Installation et Utilisation

1.  **Clonage du dépôt :**
    ```bash
    git clone [https://github.com/fahd-ichmawin03/predire_le_taux_de_sans-abris.git](https://github.com/fahd-ichmawin03/predire_le_taux_de_sans-abris.git)
    ```
2.  **Préparation des données :** S'assurer que les fichiers `train.csv` et `test.csv` sont présents pour l'application des transformations `StandardScaler`.
3.  **Soumission :** Le script final génère un fichier `submission_final_team.csv` prêt pour l'évaluation.

---

## Équipe de Projet
* **Fahd Ichmawin** 
* Abdelsalam Alhadj Ousmane
* Ilham Elouarzadi 
* Abdellatif Mahamat Dougouye
* Yousra Benkhalifa 

**Encadré par :** Pr. ABOUTABIT 
**Année Universitaire :** 2025-2026