# Report – Exploratory Analysis + LLM Insights (Retail Marketing)

This report presents: (1) The typical customer profile and (2) their consumption habits (products & channels).
We combine statistical analysis (**mean, median, standard deviation) and a local LLM (Mistral) reasoning.**

1) ## Data & Cleaning

    Source: Retail marketing dataset (customers, income, purchases by category, channels) from Kaggle.

    Key cleaning steps: Removal of outliers (YOLO, Absurd), control of extreme incomes, **creation of new variables** (Total_Purchases, Nb_Children), aggregates by marital status and education.

    Derived files: 01_overall.csv, 02_client_median_profile.csv, 03_par_statut_marital.csv, 04_par_education.csv.

2) ## Global Statistics (Educational)

    Median Income: ~ €51,373

    Average Income: ~ €51,955

    Income Standard Deviation: ~ €21,536

    Quick interpretation: The high standard deviation indicates a wide dispersion of incomes, but the **median positions the typical customer in a modest / lower-middle class bracket.** We can conclude that this is most likely a brand like 'Leclerc' that targets low-income and lower-middle-class customers.

3) ## Median Customer (±€5k around the median)

Average consumption by category for the median customer:

    MntWines: 268.81
    
    MntFruits: 13.32
    
    MntMeatProducts: 77.16
    
    MntFishProducts: 20.58
    
    MntSweetProducts: 14.90
    
    MntGoldProds: 44.25

Reading: **The median customer focuses their spending on a few key items** (e.g., Wine, Meat), confirming a "essentials + small indulgence" shopping basket. It would have been interesting to have data on multimedia products and toys for families. Indeed, the presence or absence of children does not appear to be a key factor in interpreting the data in this study.

4) ## Social Segments (Marital Status & Education)

    By marital status: see 03_par_statut_marital.csv (income, consumption by category, channels + shares, top category).

    By education level: see 04_par_education.csv (same aggregates).

5) ## Mistral Summary – Products & Channels (from the provided aggregates)

### 5.1 Best-performing products + optimization

    Wines dominate overall (median income ~€51k).
    
    Singles / Divorced over-consume wine ⇒ push online promotions (weekends, retargeting).
    
    Married people: interest in Wine + Meat packs in-store (-10% discount on weekends).
    
    2n Cycle (education): open up to Gold + Sweets via discovery bundles.
    
    Families use the supermarket as a day out: Developing a multimedia offer could accelerate consumption.

### 5.2 Improving sales channels

    Web is high-performing (high visits/purchases) ⇒ optimize UX, personalized offers for single/divorced profiles.
    
    In-store: strengthen proximity (weekend operations, cross-selling around "wine+meat" baskets).
    
    Catalogue: low usage ⇒ reserve for niches (targeted free delivery, re-engagement for less digital segments).

### 5.3 Roadmap – Actionable Recommendations

Profile	Flagship Products	Priority Channel	**Marketing Action**
Married	Wine + Meat	In-store	**Weekend packs -10%**
Single / Divorced	Wine	Web	**Online wine promos (WE), retargeting**
2n Cycle (education)	Gold + Sweets	Web	**Targeted offers, discovery bundles**
Median Customer	Wine, Meat	Web & In-store	**Loyalty programs, value/performance offers**

6) ## Visualizations

    Income histogram.

    ![Distribution des revenus des clients](/home/romain/port_folio/port_folio_ds/analyse_exploratoire_des_données/Distribution des revenus des clients.png)

    Barplots: categories by marital status / by education.

    ![Achats moyens par niveau d'éducation](/home/romain/port_folio/port_folio_ds/analyse_exploratoire_des_données/Achats moyens par niveau d'éducation.png)

    Pie/Bar: Web / In-store / Catalogue shares by segment.

    Educational tip: show on a histogram where the mean and median fall, and explain the concept of standard deviation with a visual.

7) ## Reproducibility

    ### Calculations: outputs_marketing_stats/*.csv

    01_overall.csv

    02_client_median_profile.csv

    03_par_statut_marital.csv

    04_par_education.csv

    Final Mistral prompt: prompt_mistral_final.txt (response integrated in §5)

    'You are a marketing analyst. You are provided with a pre-aggregated numerical extract.
    Base ALL your analysis ONLY on this data (no invention).

    OBJECTIVES (answer in 2 clear sections):

        Best-performing products according to status (marital & education) and how to optimize (promo, average basket, cross-sell, upsell, targeting).
        
        Improvements to sales channels (web / in-store / catalogue) taking into account the socio-economic profile (median income, dispersion) and the consumed categories.

    ### CONSTRAINTS:

        Be concise and structured.
        
        Cite key figures (median, means, channel shares) when they justify a recommendation.
        
        Give actionable recommendations (e.g., "target Married with Wine+Meat packs in-store, 10% discount on weekends").

    DATA:
    === 02 – Median customer profile (±€5000 around the median income) ===
    revenu_median_global,taille_echantillon,moy_MntWines,moy_MntFruits,moy_MntMeatProducts,moy_MntFishProducts,moy_MntSweetProducts,moy_MntGoldProds
    51373.0,313,268.814696485623,13.319488817891374,77.15654952076677,20.5814696485623,14.900958466453677,44.25239616613418

    === 03 – Aggregates by marital status (income, consumption by category, channels + shares) ===
    Marital_Status,median,mean,std,count,MntWines,MntFruits,MntMeatProducts,MntFishProducts,MntSweetProducts,MntGoldProds,NumWebPurchases,NumStorePurchases,NumCatalogPurchases,NumWebPurchases_share,NumStorePurchases_share,NumCatalogPurchases_share,top_categorie
    Alone,35860.0,43789.0,15215.133486105207,3,184.66666666666663,4.0,26.33333333333333,7.666666666666667,7.0,27.0,5.0,4.0,0.6666666666666666,0.5172413793103449,0.4137931034482759,0.0689655172413793,MntWines
    Divorced,52683.0,52834.22844827586,21239.759765284056,232,324.8448275862069,27.42672413793104,150.20689655172413,35.043103448275865,26.81896551724138,46.28879310344828,4.310344827586207,5.818965517241379,2.6724137931034484,0.3367003367003367,0.4545454545454545,0.2087542087542087,MntWines
    Married,51876.0,51724.97899649942,21449.4064042112,857,299.85530921820305,25.6487747957993,160.89614935822638,35.46674445740957,26.751458576429403,42.84597432905484,4.085180863477246,5.849474912485414,2.6301050175029173,0.325130014858841,0.4655460624071322,0.2093239227340267,MntWines
    Single,48904.0,50995.35031847134,22229.542143101145,471,291.3312101910828,27.26114649681529,184.8492569002123,38.7728237791932,27.072186836518046,43.30573248407644,3.851380042462845,5.677282377919321,2.632696390658174,0.3166899441340782,0.4668296089385475,0.2164804469273743,MntWines
    Together,51369.0,52173.12062937063,21766.10581680852,572,308.92657342657344,25.52097902097902,166.7062937062937,39.11713286713287,26.276223776223777,43.25524475524475,4.104895104895105,5.760489510489511,2.6818181818181817,0.3271561933955692,0.4591054758255538,0.2137383307788769,MntWines
    Widow,56551.0,56481.55263157895,16837.952451447087,76,367.1315789473685,31.86842105263158,185.32894736842104,49.9078947368421,37.86842105263158,55.85526315789474,4.618421052631579,6.355263157894737,3.3026315789473686,0.3235023041474654,0.4451612903225807,0.2313364055299539,MntWines

    === 04 – Aggregates by education level (income, consumption by category, channels + shares) ===
    Education,median,mean,std,count,MntWines,MntFruits,MntMeatProducts,MntFishProducts,MntSweetProducts,MntGoldProds,NumWebPurchases,NumStorePurchases,NumCatalogPurchases,NumWebPurchases_share,NumStorePurchases_share,NumCatalogPurchases_share,top_categorie
    2n Cycle,46805.0,47633.19,22119.08183787594,200,200.845,29.36,135.08,48.04,34.725,46.88,3.765,5.56,2.355,0.3223458904109589,0.4760273972602739,0.2016267123287671,MntWines
    Basic,20744.0,20306.25925925926,6235.066773288437,54,7.24074074074074,11.11111111111111,11.444444444444445,17.055555555555557,12.11111111111111,22.83333333333333,1.8888888888888888,2.851851851851852,0.4814814814814814,0.3617021276595744,0.5460992907801417,0.0921985815602836,MntGoldProds
    Graduation,51965.5,52145.44614003591,21348.474817943134,1114,285.12657091561937,30.81238779174147,180.58886894075405,43.297127468581685,31.286355475763017,50.54398563734291,4.11669658886894,5.842908438061041,2.7333931777378817,0.3243281471004243,0.4603253182461103,0.2153465346534653,MntWines
    Master,50920.5,52883.00274725275,20174.721023670005,364,333.2362637362637,21.25,161.9945054945055,31.032967032967036,20.865384615384617,39.85164835164835,4.038461538461538,5.887362637362638,2.5384615384615383,0.3240026449195504,0.4723385497024466,0.2036588053780031,MntWines
    PhD,55212.0,56177.51983298539,20650.00663780383,479,407.5782881002088,20.21711899791232,170.23799582463465,26.97286012526096,20.419624217119,32.363256784968684,4.421711899791232,6.073068893528184,2.9958246346555324,0.3277623026926648,0.4501702259362427,0.2220674713710925,MntWines

    END OF DATA — PROVIDE YOUR ANALYSIS IN 2 SECTIONS.'

    Local model: Mistral via Ollama (/api/generate)

Contact & credits: Analysis by Romain – local LLM + data science demonstration.