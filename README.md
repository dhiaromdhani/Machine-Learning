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
matching_score = (50 × skill_overlap)
+ (20 × AI_Score / 100)
+ (30 × experience_match_ratio)

experience_match_ratio = max(0, 1 - |exp_diff| / 3)
skill_overlap = skills_communs / skills_requis

→ Score ∈ [0, 100]
→ Score ≥ 50 : recommandé pour entretien


Règle de décision Good/Poor Match : `skill_overlap > 40%` ET `écart d'expérience < 3 ans`

##  Architecture technique

- Frontend : HTML/CSS/JavaScript vanilla (SPA à onglets, sans framework)
- Visualisation : Chart.js (bar, line, scatter — courbes ROC, PCA, feature importance, matrices de confusion)
- Simulation : les prédictions et l'entraînement des modèles sont simulés côté client (formules reproduisant le comportement des modèles entraînés en amont, sans appel backend/API)
- Sections du dashboard :
  - Vue d'ensemble (statut des 7 modèles + 3 PCA, performance comparative)
  - Comparaison des modèles (tableau récapitulatif global, recommandations)
  - Entraînement (simulation visuelle du pipeline complet)
  - Pour chaque objectif : modèle & métriques, analyse PCA, formulaire de prédiction interactif

## Utilisation

1. Ouvrir le fichier HTML dans un navigateur
2. Naviguer entre les 3 objectifs via la sidebar
3. Onglet "Entraînement" : lancer la simulation du pipeline (7 modèles + 3 PCA)
4. Onglets "Prédire" : ajuster le profil candidat / l'offre (expérience, AI Score, skills, éducation…) et lancer la prédiction pour voir le verdict, les probabilités et le score de matching

## Recommandations finales

- SVM (RBF) → meilleur AUC-ROC (0.94), robuste en haute dimension → sélection finale
- XGBoost → meilleur R² (0.91), capture les relations non-linéaires → scoring de matching
- Decision Tree → règles IF-THEN directement lisibles par les RH → explicabilité

##  Auteurs

Groupe 6 — FullStackers
Module Machine Learning Appliqué — Dr. Jihen Hlel
