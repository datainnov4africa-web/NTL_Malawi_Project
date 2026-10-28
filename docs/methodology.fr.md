<p align="right"><a href="methodology.md">English</a></p>

# Méthodologie — Malawi (2014–2025)

## Données et nettoyage

VIIRS DNB mensuel (VCMSLCFG) et annuel VNL V2, DMSP–VIIRS harmonisé, Black Marble quotidien, GHSL/WorldPop, Sentinel-5P NO₂/SO₂, MODIS LST, Banque mondiale. Nettoyage : pixels valides si cf_cvg ≥ 2, unité-mois gardée si ≥ 80 % de pixels observés, pics remplacés, fond et torchères masqués.

## 📈 Cas d'usage 1 — Dynamiques temporelles

- **Question** — L'activité accélère-t-elle ou ralentit-elle, hors effet de saison ?
- **Données** — VIIRS VCMSLCFG (monthly), VIIRS VNL V2 (annual), Harmonised DMSP–VIIRS (Li et al., 2020)
- **Méthode** — STL robuste (période 12) sur log(somme des lumières) ; pente de Theil–Sen et test de Mann–Kendall sur les composites annuels ; détection d'anomalies et de ruptures.
- **Validation** — Significativité de la tendance (Mann–Kendall) et cohérence mensuel/annuel (**p-value = 0,0002**)
- **Incertitude** — IC 95 % de la croissance annuelle : +2,6 % à +6,8 %
- **Limites** — Couverture nuageuse et nuits courtes en été ; la lumière n'est pas la valeur ajoutée.
- **Statut** — `experimental` · Confiance: élevée
- **Références** — Cleveland et al. (1990) STL ; Sen (1968) ; Elvidge et al. (2017).
- **Page du tableau de bord** — [`#time`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/fr/?country=MWI#time)

**Résultats de cette exécution**

- `F02` Entre 2014 et 2025, la lumière nocturne de Malawi a évolué de +5,0 % par an (IC 95 % : +2,6 % à +6,8 %). Sur les 12 derniers mois, le niveau désaisonnalisé est -2,6 % par rapport aux 12 mois précédents. (confiance élevée : tendance significative (p < 0,01 ; n = 12))
- `F54` Validation : Significativité de la tendance (Mann–Kendall) et cohérence mensuel/annuel (p-value = 0,0002). Incertitude : IC 95 % de la croissance annuelle : +2,6 % à +6,8 % Limites : Couverture nuageuse et nuits courtes en été ; la lumière n'est pas la valeur ajoutée. Statut : statistique expérimentale ; confiance élevée.

## 🗺️ Cas d'usage 2 — Croissance régionale et convergence

- **Question** — Quelles régions décollent, lesquelles décrochent ?
- **Données** — VIIRS VNL V2, GHSL / WorldPop, Sentinel-5P NO₂
- **Méthode** — Croissance robuste par unité (Theil–Sen, Mann–Kendall), classes croissance/stagnation/déclin, β- et σ-convergence, indice de Herfindahl.
- **Validation** — Corrélation de rang avec le NO₂ troposphérique (source indépendante) (**Spearman ρ = 0,15**)
- **Incertitude** — Classe attribuée seulement si |pente| ≥ seuil et p < α ; IC de β (erreurs robustes).
- **Limites** — Petites unités : bruit et débordement de lumière (blooming) entre voisins.
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Barro et Sala-i-Martin (1992) convergence ; Henderson, Storeygard et Weil (2012).
- **Page du tableau de bord** — [`#regions`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/fr/?country=MWI#regions)

**Résultats de cette exécution**

- `F03` Sur 28 unités ADM2, 25 sont en croissance significative, 3 stagnent et 0 déclinent. L'activité lumineuse reste concentrée : Central Region concentre 48 % de la lumière nationale. (confiance moyenne : classement sur 28 unités, seuil ±1 %/an et p < 0,10)
- `F04` Entre unités ADM2, la lumière par habitant converge : les unités les moins éclairées rattrapent leur retard. (confiance moyenne : β = −0,023 [−0,032 ; −0,014], n = 27)
- `F24` Central Region (ADM1, 2025) : part de la lumière nationale 48,4 %, croissance annuelle +5,9 % (IC +3,7 % à +8,2 %, classe Croissance), lumière par habitant 0,045, population 0,47 M, dans le noir 66 %, PIB estimé (expérimental) 5,90 Md USD.
- `F25` Southern Region (ADM1, 2025) : part de la lumière nationale 40,4 %, croissance annuelle +3,6 % (IC +0,1 % à +5,4 %, classe Croissance), lumière par habitant 0,039, population 0,45 M, dans le noir 68 %, PIB estimé (expérimental) 4,92 Md USD.

## 💹 Cas d'usage 3 — Relation lumières–PIB

- **Question** — Peut-on estimer la croissance avant sa publication, et le PIB régional ?
- **Données** — VIIRS, PIB réel (Banque mondiale, WDI)
- **Méthode** — log(lumière) ~ log(PIB) en niveaux et en croissance, MCO avec écarts-types HAC ; prévision hors échantillon ; PIB régional = PIB national réparti au prorata de la lumière.
- **Validation** — Suivi hors échantillon de la croissance officielle (**corrélation / EAM (points) = -0,22 / 2,2**)
- **Incertitude** — IC 95 % de l'élasticité : 0,75 à 2,11 ; intervalles de prévision 80 % et 95 %.
- **Limites** — Échantillon annuel court ; le PIB régional est une statistique expérimentale à confronter aux comptes régionaux.
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Henderson et al. (2012) AER ; Chen et Nordhaus (2011) PNAS ; Gibson et al. (2021) JDE.
- **Page du tableau de bord** — [`#time`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/fr/?country=MWI#time)

**Résultats de cette exécution**

- `F05` L'élasticité de la lumière au PIB réel est de 1,43 en niveaux (IC 95 % : 0,75 à 2,11, R² = 0,69, 12 années) et de 0,56 en taux de croissance (IC : −3,44 à 4,56). Hors échantillon, la croissance des lumières suit celle du PIB avec une corrélation de −0,22 (erreur absolue moyenne : 2,2 point de croissance). (confiance moyenne : n = 12, significatif mais IC large (1,36))
- `F30` Élasticité lumières–PIB réel en niveaux : β = 1,43 (IC 95 % 0,75 à 2,11, R² = 0,69, n = 12, confiance moyenne : n = 12, significatif mais IC large (1,36)). +1 % de PIB ↔ +β % de lumière.
- `F31` Élasticité lumières–PIB réel en taux de croissance : β = 0,56 (IC 95 % -3,44 à 4,56, R² = 0,01, n = 11, confiance faible : n = 11, non significatif (p = 0,78)). +1 % de PIB ↔ +β % de lumière.
- `F32` Élasticité lumières–PIB réel en série longue DMSP–VIIRS : β = 1,06 (IC 95 % 0,72 à 1,40, R² = 0,83, n = 30, confiance élevée : n = 30, p < 0,01, IC étroit). +1 % de PIB ↔ +β % de lumière.

## ⚡ Cas d'usage 4 — Chocs et résilience

- **Question** — Quelle a été la profondeur d'un choc, et la vitesse de récupération ?
- **Données** — VIIRS (monthly), Black Marble VNP46A2 (daily), catalogue d'événements
- **Méthode** — Écart au niveau d'avant-choc sur la série désaisonnalisée ; ruptures structurelles ; indice quotidien Black Marble.
- **Validation** — Le creux dépasse-t-il la variabilité ordinaire ? (**creux (choc principal) = 2,6 % — non**)
- **Incertitude** — Variabilité mensuelle d'avant-choc (écart-type robuste) ; ruptures inexpliquées signalées.
- **Limites** — Les chocs touchant des activités peu éclairées (agriculture, services de jour) sont sous-estimés.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Román et al. (2018) ; Elvidge et al. (2020) lumières et confinements.
- **Page du tableau de bord** — [`#shocks`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/fr/?country=MWI#shocks)

**Résultats de cette exécution**

- `F06` Le choc le plus marqué dans la série désaisonnalisée est « COVID-19 » : creux de +2,6 % (09/2020), retour au niveau d'avant-choc après 7 mois. (confiance faible : creux comparé à la variabilité mensuelle d'avant-choc)
- `F34` COVID-19 (2020-03-01 → 2021-06-30) : creux de 2,6 % le 2020-09-01, retour au niveau d'avant-choc après 7 mois. Distinct du bruit : non.
- `F35` Ruptures structurelles : 2015-11-01 (5,9 %); 2017-02-01 (35,5 %); 2021-04-01 (13,4 %). Sans événement connu à ±6 mois : 2.
- `F36` Régions les plus touchées (creux) : Central Region -21,5 % (covid19), Northern Region -0,4 % (covid19), Southern Region 0,8 % (covid19).

## ⚖️ Cas d'usage 5 — Inégalités et électrification

- **Question** — Où vivent les populations privées d'électricité ?
- **Données** — VIIRS VNL V2, GHSL / WorldPop, GHSL SMOD, accès à l'électricité (WDI)
- **Méthode** — Gini et Theil pondérés par la population ; population des pixels habités sous le seuil de détection ; sensibilité à trois seuils ; IC bootstrap de la variation du Gini.
- **Validation** — Écart avec le taux d'accès à l'électricité de la Banque mondiale (**écart moyen (points) = 17,5**)
- **Incertitude** — Plage selon le seuil de radiance ; IC bootstrap du Gini.
- **Limites** — Proxy de l'éclairage extérieur, pas du raccordement : un foyer raccordé mais peu éclairé paraît « dans le noir ».
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Theil (1967) ; Falchetta et al. (2020) accès à l'électricité par les lumières.
- **Page du tableau de bord** — [`#inequality`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/fr/?country=MWI#inequality)

**Résultats de cette exécution**

- `F07` Le Gini de la lumière par habitant (ADM2) vaut 0,42 en 2025 (évolution non significative depuis 2014). Environ 0,52 million(s) de personnes vivent dans des zones habitées sans lumière détectable (66 % de la population habitée). (confiance moyenne : sensible au seuil de radiance (de 0,48 à 0,57 M selon le seuil) ; proxy d'éclairage extérieur, pas de raccordement)
- `F37` Gini de la lumière par habitant (ADM2) : 0,491 en 2014 → 0,424 en 2025 (variation -0,067, IC bootstrap -0,114 à 0,008). Theil T 0,308 ; part entre régions 3 %.
- `F38` Habitants de zones habitées sans lumière détectable : 0,39 M (71 %) en 2014 → 0,52 M (66 %) en 2025. Rapport lumière/hab. urbain/rural 1,8. Proxy de l'accès à l'électricité, sensible au seuil.
- `F39` Écart moyen entre la part de la population en zone éclairée et le taux d'accès à l'électricité de la Banque mondiale : 17,5 points.

## 🏭 Cas d'usage 6 — Zones industrielles

- **Question** — Où est l'industrie, et son activité progresse-t-elle ?
- **Données** — VIIRS VNL V2, GHSL BUILT-S, Sentinel-5P NO₂/SO₂, MODIS MOD11A2, OpenStreetMap
- **Méthode** — Concordance de six signaux par pixel (≥ 3 dont la lumière), grappes 8-connexes, typologie et confiance.
- **Validation** — Comparaison avec la liste de référence (OpenStreetMap) (**précision / rappel / F1 = 55 % / 27 % / 0,36**)
- **Incertitude** — Confiance par grappe selon le nombre de signaux forts ; sites isolés à vérifier.
- **Limites** — Résolution de Sentinel-5P (≈ 5 km) et MODIS (1 km) : les signaux qualifient un voisinage.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Elvidge et al. (2016) torchères ; Pesaresi et al. (2023) GHSL.
- **Page du tableau de bord** — [`#industry`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/fr/?country=MWI#industry)

**Résultats de cette exécution**

- `F08` 20 grappes industrielles détectées par concordance de signaux satellitaires : 11 d'industrie lourde, 6 zones d'activités et de logistique, 1 sites d'hydrocarbures et 2 sites isolés à vérifier. Elles émettent 14,0 % de la lumière nationale (dernière année) ; leur lumière évolue de +2,2 % par an. Southern Region concentre la plus forte activité industrielle. (confiance faible : précision 55 % et rappel 27 % face à la liste de référence)
- `F40` 20 grappes industrielles (≥ 3 signaux sur 6) : Industrie lourde 11, Zone d'activités et logistique 6, Site isolé à vérifier 2, Hydrocarbures et torchères 1. Part de la lumière nationale : 14,0 % ; croissance annuelle +2,2 %. Validation (OpenStreetMap) : précision 55 %, rappel 27 %.
- `F41` IND-001 — Site isolé à vérifier à Blantyre (Southern Region) (65.36 km², 3 signaux, confiance faible); IND-004 — Zone d'activités et logistique à Lilongwe (Central Region) (3.655 km², 3 signaux, confiance faible); IND-002 — Industrie lourde à Mzimba (Northern Region) (6.235 km², 3 signaux, confiance faible); IND-007 — Zone d'activités et logistique à Lilongwe (Central Region) (1.935 km², 3 signaux, confiance faible); IND-005 — Industrie lourde à Nkhotakota (Central Region) (3.225 km², 3 signaux, confiance faible); IND-011 — Zone d'activités et logistique à Lilongwe (Central Region) (1.72 km², 3 signaux, confiance faible); IND-006 — Zone d'activités et logistique à Lilongwe (Central Region) (1.935 km², 3 signaux, confiance faible); IND-003 — Industrie lourde à Mzimba (Northern Region) (3.655 km², 3 signaux, confiance faible); IND-010 — Hydrocarbures et torchères à Karonga (Northern Region) (1.72 km², 3 signaux, confiance faible); IND-009 — Industrie lourde à Chikwawa (Southern Region) (1.935 km², 4 signaux, confiance moyenne)
- `F42` Southern Region : 8 grappe(s) industrielle(s), 73,7 km², 25,2 % de la lumière de la région.

## 🏖️ Cas d'usage 7 — Tourisme saisonnier

- **Question** — Quelles zones vivent du tourisme, et comment évolue la saison ?
- **Données** — VIIRS (monthly), nuitées ou arrivées WDI
- **Méthode** — Surcroît estival net des unités comparables de même latitude ; test unilatéral ; indice de saison base 100 ; saisons recoupant le Ramadan signalées.
- **Validation** — Corrélation avec international tourist arrivals (WDI) (**r = -0,96**)
- **Incertitude** — p-valeur par unité ; années 2020–2021 exclues du classement.
- **Limites** — Toute activité estivale (diaspora, résidences secondaires, festivals) est captée, pas seulement le tourisme.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Analyses saisonnières des lumières et du tourisme, par ex. Hu et al. (2021).
- **Page du tableau de bord** — [`#tourism`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/fr/?country=MWI#tourism)

**Résultats de cette exécution**

- `F09` 2 unités sur 28 ont un surcroît de lumière estival net d'au moins 10 % : Nkhotakota (Central Region), Mzimba (Northern Region). Le surcroît net médian atteint +21 % dans la zone la plus touristique. L'indice de saison (base 100 = 2019) tombe à 109 en 2020 et vaut -61 en 2025. (confiance faible : corrélation de -0,96 avec international tourist arrivals (WDI) (4 années))
- `F46` 2 zone(s) touristique(s) sur 28 unités ADM2 (surcroît estival net ≥ 10 %, mois de pointe [12, 1]) : Nkhotakota (Central Region) (+21 %, confiance moyenne), Mzimba (Northern Region) (+12 %, confiance moyenne).
- `F47` Indice de saison (base 100 = 2019) : 2015 : 353, 2016 : 131, 2017 : 273, 2018 : 69, 2019 : 100, 2020 : 109, 2021 : -614, 2022 : 196, 2024 : 362, 2025 : -61. Années avec Ramadan chevauchant la saison : 2021, 2022, 2024, 2025.
- `F48` Corrélation entre l'indice de saison et international tourist arrivals (WDI) : -0,96 (4 années ; en croissance : n.d.).

## 🏙️ Cas d'usage 8 — Signaux d'urbanisation

- **Question** — Où les villes s'étendent-elles, où les villages s'électrifient-ils, et où la population croît-elle sans lumière ?
- **Données** — VIIRS VNL V2, GHSL GHS-POP / WorldPop, GHSL GHS-BUILT-S R2023A, population urbaine (WDI)
- **Méthode** — Surface éclairée (pixels au-dessus du seuil) et population par unité ; croissances de Theil–Sen ; pixels nouvellement éclairés (sombres deux années de suite au début, éclairés deux années de suite à la fin), séparés entre électrification de zones habitées et nouvelles implantations ; typologie lumière/population.
- **Validation** — Corrélation de rang avec la croissance de la surface bâtie GHSL (source indépendante) (**Spearman ρ = 0,09**)
- **Incertitude** — Persistance exigée sur deux années pour limiter le bruit ; marge de ± 1 point entre croissances avant de classer.
- **Limites** — La lumière mesure l'éclairage extérieur, pas l'urbanisation au sens administratif ; le débordement (blooming) élargit les villes ; la population GHSL est interpolée entre époques.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Zhou et al. (2015) étendue urbaine par les lumières ; Pesaresi et al. (2023) GHSL ; Min et al. (2013) électrification des villages.
- **Page du tableau de bord** — [`#urban`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/fr/?country=MWI#urban)

**Résultats de cette exécution**

- `F49` Surface éclairée nationale : +8,6 % par an ; population : +2,7 % par an. Classes (ADM2) : Urbanisation électrifiée 27, Croissance équilibrée 1.
- `F50` Entre 2014 et 2025 : 1 743 km² nouvellement éclairés, dont 489 km² de zones déjà habitées (électrification, ≈ 36 k habitants) et 1 254 km² de nouvelles implantations ; 30 km² ont perdu leur lumière.
- `F51` Plus forte extension de la surface éclairée : Chiradzulu (Southern Region) (+16,6 %/an), Nkhata Bay (Northern Region) (+15,1 %/an), Nkhotakota (Central Region) (+15,0 %/an), Dowa (Central Region) (+14,6 %/an), Chitipa (Northern Region) (+13,7 %/an), Phalombe (Southern Region) (+12,6 %/an). Croissance non éclairée (population plus rapide que la lumière) : aucune.
- `F52` Corrélation de rang (Spearman) entre croissance de la surface éclairée et croissance du bâti GHSL : 0,09 (p = 0,664, 28 unités).

## Limites générales des lumières nocturnes

- **Ce que mesurent les lumières** — Radiance émise vers le haut vers 01 h 30 : l'agriculture, le commerce de jour, les services peu éclairés et l'économie informelle rurale sont mal captés.
- **Saturation et débordement** — DMSP sature au centre des villes (DN 63) et « déborde » (blooming) ; VIIRS est bien meilleur mais le débordement gonfle encore la surface éclairée des villes.
- **Torchères et sites isolés** — Le masque automatique peut retirer des mines, ports ou centrales isolés, et manquer de petites torchères ; les candidats sont exportés pour vérification.
- **Nuages, saisons, lune** — Les mois nuageux sont partiellement observés ; la STL retire la saisonnalité moyenne mais pas une saison anormale (neige, mousson tardive).
- **Ruptures de produit** — DMSP et VIIRS ne sont pas directement comparables : la série longue harmonisée (Li et al., 2020) est un produit modélisé, à lire en tendance seulement.
- **Élasticité NTL–PIB** — Estimée sur 10 à 30 points annuels : intervalles larges, instabilité possible, relation non causale et variable selon le niveau de développement.
- **Accès à l'électricité** — « Habité sans lumière » ≠ « non raccordé » : un foyer raccordé à faible consommation est invisible ; l'indicateur dépend fortement du seuil de radiance et de la population.
- **Limites administratives** — geoBoundaries/GAUL peuvent différer des limites officielles ; les petites unités ADM2 sont sensibles au débordement de la lumière des voisines.
- **Zones industrielles** — La détection repose sur des seuils : une centrale, un port ou un grand centre commercial peut cumuler les signaux ; une usine peu éclairée ou sans émissions visibles échappe à la détection. Sentinel-5P (≈ 5 km) et MODIS (1 km) sont plus grossiers que VIIRS : les signaux NO₂/SO₂/chaleur qualifient un voisinage, pas un bâtiment.
- **Tourisme estival** — Le surcroît estival mesure toute hausse de lumière en été (résidences secondaires, diaspora, fêtes, chantiers), pas seulement le tourisme ; aux hautes latitudes, les nuits d'été très courtes réduisent les observations VIIRS. Le Ramadan modifie l'activité nocturne : les étés concernés sont signalés.
- **Urbanisation** — La surface éclairée dépend du seuil de détection et du débordement de lumière (blooming) autour des villes ; un quartier raccordé mais peu éclairé reste invisible. La population (GHSL/WorldPop) est modélisée à partir des recensements : sa croissance n'est pas une observation indépendante, et les années entre deux millésimes sont interpolées.


---
<sub>Généré par le notebook le 2026-10-28 · version 2.1.0</sub>
