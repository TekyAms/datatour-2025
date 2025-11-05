# 🏆 Ma Participation au DataTour 2025 - Challenge Credit Scoring

Ce dépôt contient ma solution développée lors de ma participation au challenge de Credit Scoring du DataTour 2025. Le défi consistait à prédire les risques de défaut de paiement en utilisant des données historiques de comportement client.

## 🎯 Le Challenge

- **Objectif** : Prédire les probabilités de défaut de paiement
- **Métrique** : Score AUC (Area Under the Curve)
- **Données** : Historique de paiement et caractéristiques des clients
- **Particularité** : Fort déséquilibre des classes (~29:1)

## 📊 Approche Adoptée

### Développement Itératif
1. **Fichier initial fourni** (`base_code.ipynb`)
   - Notebook fourni par les organisateurs (starter kit)
   - Implémentation basique avec régression logistique
   - Score AUC baseline : 0.574

2. **Ma Solution Progressive** (`complete_solution.ipynb`)
   - Première étape : Implémentation avec LightGBM
     - Features engineering initial
     - Score AUC : 0.65417 (gain de +0.08 points !)
   
   - Deuxième étape : Exploration multi-modèles
     - Implémentation de XGBoost pour comparaison
     - Ajout de CatBoost comme troisième approche
     - Objectif : identifier le modèle le plus performant
     - Création d'un ensemble des trois modèles

### 🔧 Points Clés de la Solution
- Features temporelles avancées
- Agrégations intelligentes par client
- Target encoding optimisé
- Approche ensemble multi-modèles
- Validation croisée à 5 folds

## 📈 Résultats

- **Score de Base** (LightGBM) : 0.65417
- **Features Engineering** :
  - Analyse temporelle des comportements
  - Agrégation des historiques clients
  - Encodage des variables catégorielles
  - Création de features d'interaction