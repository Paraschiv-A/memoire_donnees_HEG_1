# Dossier data/

Ce dossier contient les fichiers de données lus et produits par les notebooks.

## À déposer ici

- **`bofip_stock_live_20260521.tgz`** : l'archive du stock BOFiP (environ 297 Mo).
  Non versionnée sur GitHub (trop volumineuse). À retélécharger à la source
  (https://www.data.gouv.fr, jeu de données BOFiP de la DGFiP) et à placer ici.

## Fichiers dérivés (peuvent être versionnés)

- `inventaire_bofip_stock_live_20260521.csv` et `.xlsx` : inventaire produit par le
  notebook `01_profilage_bofip_consolide`.
- `coquilles_filtrees_20260630_084651.csv` : liste filtrée des coquilles (retraits et
  transferts), utilisée par `05_voir_coquilles`. Fichier dérivé d'open data, déposable tel quel.

Les autres sorties (`representants_par_type.csv`, `synthese_par_type.csv`,
`mesure_par_document_types_mineurs.csv`, etc.) sont régénérées à l'exécution des notebooks.
