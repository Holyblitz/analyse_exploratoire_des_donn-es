# analyse_exploratoire_des_données

# Analyse des comportements d'achat selon le profil client

## 📌 Description
Ce projet analyse un dataset client (segments 2 à 4) afin d’identifier :
1. Les produits les plus performants selon le statut marital et le niveau d’éducation.
2. Les optimisations possibles sur les produits.
3. Les pistes d’amélioration des canaux de vente.

Les données ont été traitées en Python puis analysées avec un LLM (Mistral) pour formuler des recommandations précises.

---

## 📊 Résultats principaux

### 1. Optimisation des produits selon le statut marital et l'éducation
- **Produits phares** : Le vin est le produit le plus consommé (moyenne : 268,81 unités, revenu médian : 51 373 €).
- **Impact du statut marital** :
  - Clients **célibataires ou divorcés** → consommation plus élevée de vin.
  - Clients **mariés** → consommation plus équilibrée, davantage orientée vers la viande et les produits combinés.
- **Impact du niveau d’éducation** :
  - Les diplômés du 2nd cycle sont plus sensibles aux offres sur les produits d’or et les sucreries.

**Recommandations :**
- Packs Vin + Viande en magasin pour clients mariés (remise 10% le week-end).
- Enchères en ligne sur le vin pour célibataires/divorcés.
- Offres ciblées sur produits d’or et sucreries pour diplômés du 2nd cycle.

---

### 2. Amélioration des canaux de vente
- **Tendances observées** :
  - Revenus ~5 000 € → forte utilisation du web et du magasin.
  - Canal catalogue peu exploité.
  - Célibataires/divorcés → plus actifs sur web et magasin.
  - Clients solitaires → plus enclins au catalogue.

**Recommandations :**
- Expérience web enrichie et promotions pour célibataires/divorcés.
- Livraison gratuite sur le canal catalogue pour clients solitaires.
- Ouverture de magasins dans zones à forte population de clients mariés.

---

## 📈 Visualisations

| Distribution des revenus | Achats par éducation | Achats par statut marital | Consommation par canal |
|--------------------------|----------------------|---------------------------|------------------------|
| ![Revenus](images/revenus.png) | ![Éducation](images/education.png) | ![Statut marital](images/statut_marital.png) | ![Canaux](images/canaux.png) |

---

## 🛠️ Technologies utilisées
- Python (pandas, matplotlib)
- Mistral (analyse et recommandations)
- Jupyter Notebook

---

## 📂 Structure du dépôt

.
├── data/ # CSV nettoyés
├── images/ # Graphiques générés
├── README_fr.md
├── README_en.md
└── analysis.ipynb


---

## ✍️ Auteur
Projet réalisé par **Romain** dans le cadre de son portfolio Data Science.
