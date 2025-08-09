
# Rapport – Analyse exploratoire + insights LLM (Marketing Retail)

Ce rapport présente : (1) **Qui est le client type** et (2) **comment il consomme** (produits & canaux).
Nous combinons une analyse **statistique** (moyenne, médiane, écart-type) et un **raisonnement LLM local (Mistral)**.

---

## 1) Données & nettoyage
- Source : dataset marketing retail (clients, revenus, achats par catégorie, canaux) sur kaggle.
- Nettoyages clés : suppression des valeurs aberrantes (`YOLO`, `Absurd`), contrôle des revenus extrêmes, création de variables (Total_Purchases, Nb_Enfants), agrégats par statut et éducation.
- Fichiers dérivés : `01_overall.csv`, `02_client_median_profile.csv`, `03_par_statut_marital.csv`, `04_par_education.csv`.

## 2) Statistiques globales (pédagogie)
- **Revenu médian** : ~ **51,373 €**
- **Revenu moyen** : ~ **51,955 €**
- **Écart-type des revenus** : ~ **21,536 €**

> _Interprétation rapide_ : écart-type élevé ⇒ forte dispersion des revenus, mais la médiane positionne le **client type** dans une classe **modeste / moyenne inférieure**. Nous pouvons conclure qu'il s'agit très probablement d'une enseigne type 'Leclerc' qui a comme cible de marché les faibles revenus et le début de la classe moyenne.

## 3) Client médian (±5k€ autour de la médiane)
Consommation moyenne par catégorie du client médian :
- **MntWines** : 268.81
- **MntFruits** : 13.32
- **MntMeatProducts** : 77.16
- **MntFishProducts** : 20.58
- **MntSweetProducts** : 14.90
- **MntGoldProds** : 44.25

**Lecture** : le client médian concentre ses dépenses sur quelques postes clés (ex. _Vin_, _Viande_), confirmant un panier “essentiels + petit plaisir”. Il aurait été intéressant d'avoir des données sur les produits multimédias et jouets pour les familles. En effet le fait d'avoir des enfants ou non n’apparaît pas dans cette étude comme un facteur clé d’interprétation des données.

## 4) Segments sociaux (statut marital & éducation)
- Par **statut marital** : voir `03_par_statut_marital.csv` (revenus, conso par catégorie, canaux + parts, top catégorie).
- Par **niveau d’éducation** : voir `04_par_education.csv` (mêmes agrégats).

---

## 5) Synthèse Mistral – Produits & Canaux (à partir des agrégats fournis)
### 5.1 Produits qui marchent le mieux + optimisation
- **Vins** dominent globalement (revenu médian ~51k€).  
- **Célibataires / Divorcés** surconsomment **le vin** ⇒ pousser promos en **ligne** (week-end, retargeting).
- **Mariés** : intérêt pour **packs Vin + Viande** en **magasin** (remise -10% le week-end).  
- **2n Cycle** : ouvrir sur **Or + Sucré** via bundles découverte.
- **Les famille**s utilisent le supermarché comme sortie: **Développer une offre multimédia pourrait accélérer** la consommation.

### 5.2 Amélioration des canaux de vente
- **Web** performant (visites/achats élevés) ⇒ optimiser **UX**, offres **personnalisées** pour profils solos/divorcés.
- **Magasin** : renforcer proximité (opés week-end, cross-sell autour des paniers “vin+viande”).  
- **Catalogue** : usage faible ⇒ réserver aux niches (livraison gratuite ciblée, relance segments peu digitaux).

### 5.3 Tableau de route – Recommandations actionnables
| Profil | Produits phares | Canal prioritaire | Action marketing |
|---|---|---|---|
| Mariés | Vin + Viande | Magasin | Packs week-end -10% |
| Célibataires / Divorcés | Vin | Web | Promo vins en ligne (WE), retargeting |
| 2n Cycle (éducation) | Or + Sucré | Web | Offres ciblées, bundles découverte |
| Client médian | Vin, Viande | Web & Magasin | Fidélisation, offres valeur/performance |

---

## 6) Visualisations
- Histogramme revenus.

  ![Distribution des revenus des clients](/home/romain/port_folio/port_folio_ds/analyse_exploratoire_des_données/Distribution des revenus des clients.png)

- Barplots : catégories **par statut marital** / **par éducation**.

  ![achats_statut_marital](/home/romain/port_folio/port_folio_ds/analyse_exploratoire_des_données/achats_statut_marital.png)

  ![Achats moyens par niveau d'éducation](/home/romain/port_folio/port_folio_ds/analyse_exploratoire_des_données/Achats moyens par niveau d'éducation.png)

- Pie/Bar : parts **Web / Magasin / Catalogue** par segment.

  ![Achats_moyens_par_canal](/home/romain/port_folio/port_folio_ds/analyse_exploratoire_des_données/Achats_moyens_par_canal.png)

> _Astuce pédagogique_ : montrer sur un histogramme **où tombent la moyenne et la médiane**, et expliquer la notion d’écart-type avec un visuel.

---

## 7) Reproductibilité
- Calculs : `outputs_marketing_stats/*.csv`

   [01_overall.csv](/home/romain/port_folio/port_folio_ds/analyse_exploratoire_des_données/01_overall.csv) 

   [02_client_median_profile.csv](/home/romain/port_folio/port_folio_ds/analyse_exploratoire_des_données/02_client_median_profile.csv) 

   [03_par_statut_marital.csv](/home/romain/port_folio/port_folio_ds/analyse_exploratoire_des_données/03_par_statut_marital.csv) 

   [04_par_education.csv](/home/romain/port_folio/port_folio_ds/analyse_exploratoire_des_données/04_par_education.csv) 

- Prompt final Mistral : `prompt_mistral_final.txt` (réponse intégrée en §5)

  'Tu es un analyste marketing. On te fournit un extrait chiffré déjà agrégé.
  Base TOUTE ton analyse UNIQUEMENT sur ces données (pas d'invention).

  OBJECTIFS (réponds en 2 sections claires) :
  1) Produits qui marchent le mieux selon les statuts (marital & éducation) et comment optimiser (promo, panier moyen, cross-sell, upsell, ciblage).
  2) Améliorations des canaux de vente (web / magasin / catalogue) en tenant compte du profil socio-éco (revenu médian, dispersion) et des catégories consommées.

  CONTRAINTES :
  - Sois concis et structuré.
  - Cite les chiffres clés (médiane, moyennes, parts de canal) quand ils justifient une reco.
  - Donne des recommandations actionnables (ex : “cibler Married avec packs Vin+Viande en magasin, remise 10% le week-end”).

  DONNÉES :
  === 02 – Profil du client médian (±5000€ autour du revenu médian) ===
  revenu_median_global,taille_echantillon,moy_MntWines,moy_MntFruits,moy_MntMeatProducts,moy_MntFishProducts,moy_MntSweetProducts,moy_MntGoldProds
  51373.0,313,268.814696485623,13.319488817891374,77.15654952076677,20.5814696485623,14.900958466453677,44.25239616613418

  === 03 – Agrégats par statut marital (revenus, conso par catégorie, canaux + parts) ===
  Marital_Status,median,mean,std,count,MntWines,MntFruits,MntMeatProducts,MntFishProducts,MntSweetProducts,MntGoldProds,NumWebPurchases,NumStorePurchases,NumCatalogPurchases,NumWebPurchases_share,NumStorePurchases_share,NumCatalogPurchases_share,top_categorie
  Alone,35860.0,43789.0,15215.133486105207,3,184.66666666666663,4.0,26.33333333333333,7.666666666666667,7.0,27.0,5.0,4.0,0.6666666666666666,0.5172413793103449,0.4137931034482759,0.0689655172413793,MntWines
  Divorced,52683.0,52834.22844827586,21239.759765284056,232,324.8448275862069,27.42672413793104,150.20689655172413,35.043103448275865,26.81896551724138,46.28879310344828,4.310344827586207,5.818965517241379,2.6724137931034484,0.3367003367003367,0.4545454545454545,0.2087542087542087,MntWines
  Married,51876.0,51724.97899649942,21449.4064042112,857,299.85530921820305,25.6487747957993,160.89614935822638,35.46674445740957,26.751458576429403,42.84597432905484,4.085180863477246,5.849474912485414,2.6301050175029173,0.325130014858841,0.4655460624071322,0.2093239227340267,MntWines
  Single,48904.0,50995.35031847134,22229.542143101145,471,291.3312101910828,27.26114649681529,184.8492569002123,38.7728237791932,27.072186836518046,43.30573248407644,3.851380042462845,5.677282377919321,2.632696390658174,0.3166899441340782,0.4668296089385475,0.2164804469273743,MntWines
  Together,51369.0,52173.12062937063,21766.10581680852,572,308.92657342657344,25.52097902097902,166.7062937062937,39.11713286713287,26.276223776223777,43.25524475524475,4.104895104895105,5.760489510489511,2.6818181818181817,0.3271561933955692,0.4591054758255538,0.2137383307788769,MntWines
  Widow,56551.0,56481.55263157895,16837.952451447087,76,367.1315789473685,31.86842105263158,185.32894736842104,49.9078947368421,37.86842105263158,55.85526315789474,4.618421052631579,6.355263157894737,3.3026315789473686,0.3235023041474654,0.4451612903225807,0.2313364055299539,MntWines

  === 04 – Agrégats par niveau d'éducation (revenus, conso par catégorie, canaux + parts) ===
  Education,median,mean,std,count,MntWines,MntFruits,MntMeatProducts,MntFishProducts,MntSweetProducts,MntGoldProds,NumWebPurchases,NumStorePurchases,NumCatalogPurchases,NumWebPurchases_share,NumStorePurchases_share,NumCatalogPurchases_share,top_categorie
  2n Cycle,46805.0,47633.19,22119.08183787594,200,200.845,29.36,135.08,48.04,34.725,46.88,3.765,5.56,2.355,0.3223458904109589,0.4760273972602739,0.2016267123287671,MntWines
  Basic,20744.0,20306.25925925926,6235.066773288437,54,7.24074074074074,11.11111111111111,11.444444444444445,17.055555555555557,12.11111111111111,22.83333333333333,1.8888888888888888,2.851851851851852,0.4814814814814814,0.3617021276595744,0.5460992907801417,0.0921985815602836,MntGoldProds
  Graduation,51965.5,52145.44614003591,21348.474817943134,1114,285.12657091561937,30.81238779174147,180.58886894075405,43.297127468581685,31.286355475763017,50.54398563734291,4.11669658886894,5.842908438061041,2.7333931777378817,0.3243281471004243,0.4603253182461103,0.2153465346534653,MntWines
  Master,50920.5,52883.00274725275,20174.721023670005,364,333.2362637362637,21.25,161.9945054945055,31.032967032967036,20.865384615384617,39.85164835164835,4.038461538461538,5.887362637362638,2.5384615384615383,0.3240026449195504,0.4723385497024466,0.2036588053780031,MntWines
  PhD,55212.0,56177.51983298539,20650.00663780383,479,407.5782881002088,20.21711899791232,170.23799582463465,26.97286012526096,20.419624217119,32.363256784968684,4.421711899791232,6.073068893528184,2.9958246346555324,0.3277623026926648,0.4501702259362427,0.2220674713710925,MntWines


  FIN DES DONNÉES — FOURNIS TON ANALYSE EN 2 SECTIONS.'

- Modèle local : **Mistral** via Ollama (`/api/generate`)

---

_Contact & crédits :_ Analyse par Romain – démonstration LLM local + data science.
