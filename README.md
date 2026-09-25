#  HR AI Matching Platform

**Groupe 6 — FullStackers** · Module ML Appliqué · Dr. Jihen Hlel

##  Description

Plateforme de matching RH basée sur le Machine Learning, qui prédit la compatibilité entre des candidats et des offres d'emploi. Le projet combine 3 objectifs de modélisation complémentaires (classification, clustering et régression) autour d'un dataset de 100 000 paires candidat-offre, et présente les résultats dans un dashboard interactif (HTML/CSS/JS + Chart.js).

##  Objectifs du projet

###  Objectif 1 — Décision RH rapide
Classifier chaque paire candidat-offre en Good Match / Poor Match pour accélérer la présélection RH.
- Modèles : Decision Tree (max_depth=5), KNN
- Résultats : Decision Tree 88% accuracy / AUC 0.87 · KNN 86% / AUC 0.85
- PCA₁ : 63.2% de variance expliquée (2 composantes)

### 🟠 Objectif 2 — Sélection optimisée
Trouver l'hyperplan optimal de séparation (SVM) et segmenter les profils candidats en groupes homogènes (K-Means).
- Modèles : SVM (kernel RBF, C=1.0), K-Means (K=4)
- Résultats : SVM 92% accuracy / AUC 0.94 · Silhouette Score 0.5812
- Clusters : Seniors Tech, Juniors polyvalents, Profils spécialisés, Profils académiques
- PCA₂ : 63.1% de variance expliquée

### 🟢 Objectif 3 — Score de matching (0–100)
Prédire un score continu de compatibilité candidat-offre.
- Modèles : Régression Linéaire (baseline), XGBoost Regressor (n=300)
- Résultats : Régression Linéaire R²=0.79 / RMSE=8.2 · XGBoost R²=0.91 / RMSE=5.4
- PCA₃ : 62.8% de variance expliquée

##  Dataset

| Élément | Valeur |
|---|---|
| Candidats | 1 000 |
| Offres d'emploi | 500 |
| Paires générées (cross-join) | 100 000 |
| Taux de Good Match | ~30% |
| Features | 9 |

##  Feature Engineering
