# Profilage du jeu de données DVF 2022 — notebooks

*Cas d'application « apprentissage supervisé » — mémoire de master, filière Information documentaire, HES-SO / HEG Genève. Dernière mise à jour : 14.08.2026.*

## Objet du dépôt

Ce dépôt réunit les notebooks de profilage du fichier **DVF 2022** (Demandes de valeurs foncières). Ils servent de cas d'application à un mémoire portant sur la préparation et la gouvernance des données pour l'intelligence artificielle. Le fil conducteur est le rôle de *data steward* : la personne qui constate l'état des données, le documente, puis conseille les équipes techniques. Les notebooks illustrent ce travail de constat, en amont d'un modèle d'apprentissage.

Chaque notebook répond à une question simple et se lit seul. Les résultats affichés (tableaux, chiffres) sont conservés tels qu'ils ont été calculés. Pour les rejouer, il suffit de placer le fichier de données au bon endroit (voir plus bas).

## Le jeu de données

Le fichier travaillé est `dvf-2022.parquet`. C'est une version consolidée au format Parquet, préparée par icem7 à partir des données DVF de la DGFiP, et publiée sur data.gouv.fr en novembre 2023. Le fichier officiel d'origine est le fichier texte `valeursfoncieres-2022.txt`, séparé par des barres verticales.

Le fichier couvre l'année 2022 et compte 4 617 590 lignes. Une même mutation (une vente) y occupe souvent plusieurs lignes, une par bien ou par lot ; la valeur foncière, qui est le prix de la mutation entière, est alors répétée sur chacune de ces lignes. Quatre départements sont absents du fichier (57, 67, 68 et 976), car ils relèvent du Livre foncier et non du fichier DVF.

Les données DVF sont diffusées en open data, sous Licence Ouverte (Etalab).

### Le fichier de données n'est pas inclus

Le fichier `dvf-2022.parquet` **n'est pas déposé** dans ce dépôt. Il se retélécharge librement depuis data.gouv.fr. Pour exécuter les notebooks, placer le fichier dans un sous-dossier `data/` :

```
.
├── data/
│   └── dvf-2022.parquet        # à télécharger et déposer ici
├── figures/                    # créé automatiquement par le notebook de graphique
└── *.ipynb
```

Tous les chemins des notebooks sont relatifs (`./data/dvf-2022.parquet` en entrée, `./figures` en sortie). Aucun chemin absolu ni identifiant local n'y figure.

## Organisation des notebooks

Les notebooks se répartissent en deux groupes. Les notebooks de **profilage** parcourent le fichier étape par étape. Les notebooks de **vérification** ont été ajoutés pour tracer des chiffres précis cités dans le mémoire.

### Notebooks de profilage

| Notebook | Ce qu'il produit |
| --- | --- |
| `profilage_dvf_2022_etape1_decouverte` | Structure du fichier : nombre de lignes et de colonnes, types, taux de remplissage, colonnes vides. |
| `profilage_dvf_2022_etape2b_lignes_indistinguables` | Profil des lignes rendues indistinguables, par type de bien, nature de mutation et département. |
| `profilage_dvf_2022_etape2c_distributions_anomalies` | Distributions et anomalies : répartition dans le temps, valeurs extrêmes, transactions à 0 euro, valeur foncière par type, lignes sans prix. |
| `profilage_dvf_2022_etape2d_anomalies_lots_completude` | Anomalies de lots et de complétude : lignes sans code postal (VEFA), mutations sans prix, cohérence entre lots et Surface Carrez. |
| `profilage_dvf_2022_etape2e_surface_carrez_par_type` | Taux de remplissage de la Surface Carrez par type de bien. |
| `profilage_dvf_2022_etape2f_transactions_faibles` | Transactions à faible valeur : seuils de prix, populations sous 1 000 euros, biens bâtis à moins de 1 000 euros. |
| `profilage_dvf_2022_etape2g_ecart_moyenne_mediane` | Écart entre moyenne et médiane : ratio global, par type de bien, par département, et effet du retrait des valeurs extrêmes. |
| `profilage_dvf_2022_etape2h_prix_m2_valeurs_aberrantes` | Prix au mètre carré par type de bien, avec les valeurs aberrantes hautes et basses. |
| `profilage_dvf_2022_distribution_log_valeur_fonciere` | Histogramme de la valeur foncière en échelle logarithmique, avec la médiane et la moyenne. |
| `dvf_2022_lignes_indistinguables` | Lignes rendues identiques par l'expurgation : distribution des tailles de groupes et exemples concrets. |

### Notebooks de vérification

| Notebook | Ce qu'il produit |
| --- | --- |
| `profilage_dvf_2022_complements` | Distribution de la nature de mutation, nombre de départements présents (97), nombre de codes de nature de culture (27) et de nature de culture spéciale (127). |
| `profilage_dvf_2022_apercu` | Aperçu des dix premières lignes du fichier, sur six colonnes lisibles. |
| `profilage_dvf_2022_manquant_structurel` | Présence de la surface bâtie et du nombre de pièces par type de local ; montre que ces valeurs sont absentes pour la totalité des terrains nus. |
| `profilage_dvf_2022_format_carrez` | Type de stockage de la Surface Carrez (texte) comparé à la surface réelle bâtie (entier), avec les valeurs brutes à virgule décimale. |
| `exemple_abbaretz_prix_par_mutation` | Les six lignes de la mutation d'Abbaretz, au même prix et à la même adresse, dont quatre maisons de 70 m². |
| `profilage_dvf_2022_ecart_morbihan` | Origine du ratio moyenne/médiane élevé du Morbihan : mutations aux plus fortes valeurs et poids de la plus grosse dans la somme du département. |
| `profilage_dvf_2022_morbihan_deux_mutations` | Décomposition par type de bien des deux ventes en bloc du Morbihan, enregistrées le 27 décembre 2022. |

## Environnement

Les notebooks sont écrits en Python et interrogent le fichier Parquet avec DuckDB, sans le charger entièrement en mémoire. Le notebook de graphique utilise en plus matplotlib.

Installation des bibliothèques :

```bash
pip install duckdb pandas matplotlib
```

## Reproduire les résultats

1. Télécharger `dvf-2022.parquet` depuis data.gouv.fr et le déposer dans `data/`.
2. Ouvrir le notebook voulu (Jupyter, JupyterLab ou VS Code).
3. Exécuter les cellules dans l'ordre.

Un notebook qui produit une figure l'enregistre dans le dossier `figures/`, créé au besoin.

## Une note sur les résultats affichés

Les résultats visibles dans les notebooks correspondent à une exécution sur le fichier DVF 2022. Quelques notebooks courts ont été laissés sans sortie enregistrée : les rejouer sur le fichier de données produit les tableaux correspondants.
