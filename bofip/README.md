# Préparation des données et data stewardship pour l'IA — cas BOFiP (RAG)

Ce dépôt réunit les carnets d'analyse (notebooks Jupyter) réalisés dans le cadre d'un
mémoire de Master en Sciences de l'information (HES-SO / HEG Genève), mené en partenariat
avec la Direction Générale des Finances Publiques (DGFiP, France).

Le mémoire soutient que le rôle de data steward et la qualification de données prêtes pour
l'IA (AI-ready) sont des conditions préalables au déploiement de l'IA dans une administration
publique. Le corpus **BOFiP** (Bulletin Officiel des Finances Publiques) sert de terrain
concret pour le cas d'un système de génération augmentée par la recherche (RAG).

Les notebooks documentent le profilage du corpus : inventaire, structure documentaire,
renvois entre documents (dc:relation) et orphelins, coquilles (documents sans doctrine
utile), fraîcheur, longueur des documents et échantillonnage par type.

## Données et licence

Le corpus BOFiP est diffusé en open data sous **Licence Ouverte 2.0 (Etalab)**. Aucune donnée
personnelle ni secret fiscal n'est présent dans ce dépôt : les analyses portent sur de la
doctrine fiscale publique.

Le jeu de départ est l'archive **`bofip_stock_live_20260521.tgz`** (stock complet du
21.05.2026, environ 297 Mo). Cette archive **n'est pas déposée ici** en raison de sa taille
(limite GitHub de 100 Mo par fichier). Elle reste re-téléchargeable à la source :

- Portail : https://www.data.gouv.fr (jeu de données BOFiP, DGFiP)

Pour rejouer les analyses, télécharger l'archive à la source et la placer dans le dossier
`data/` (voir plus bas).

## Structure du dépôt

```
.
├── README.md
├── .gitignore
├── 01_profilage_bofip_consolide.ipynb        (+ .html)
├── 02_inventaire_fichiers_familles_bofip.ipynb
├── ...
├── 16_verifier_constat_par_type.ipynb
└── data/
    ├── bofip_stock_live_20260521.tgz          (à retélécharger, non versionné)
    ├── inventaire_bofip_stock_live_20260521.csv   (produit par le notebook 01)
    ├── inventaire_bofip_stock_live_20260521.xlsx  (produit par le notebook 01)
    └── coquilles_filtrees_20260630_084651.csv     (fichier dérivé, déposable tel quel)
```

Chaque notebook est fourni en deux formats : le `.ipynb` (code exécutable) et le `.html`
(version déjà exécutée, consultable sans rien installer).

> GitHub affiche les `.html` en code brut, pas en rendu. Pour lire un notebook exécuté
> directement dans le navigateur, coller l'adresse du `.ipynb` dans https://nbviewer.org.

## Les 16 notebooks (ordre de lecture)

1. **profilage_bofip_consolide** — inventaire consolidé du stock et profil général (types, séries, renvois, orphelins, fraîcheur). Produit l'inventaire réutilisé par les autres notebooks.
2. **inventaire_fichiers_familles_bofip** — recensement des fichiers de l'archive et des grandes familles de contenus.
3. **inventaire_fichiers_bofip** — inventaire détaillé des fichiers par document.
4. **inspecter_6_sans_sujet** — inspection des documents sans sujet (dc:subject), pages chapeau de catégories d'annexes.
5. **voir_coquilles** — vérification visuelle d'un échantillon de coquilles (avis de retrait ou de transfert, sans doctrine utile).
6. **exploration_renvois_orphelins_bofip** — analyse des renvois (dc:relation) et des orphelins par type (Actualité, Contenu, Fichier, Image).
7. **complement_renvois_bofip** — complément : documents sans aucun renvoi, rappel des totaux.
8. **extrait_fichier_8347_PGP** — extraction des fichiers d'un document témoin (8347-PGP).
9. **ouvrir_8347_et_trier_renvois_STOCK** — lecture et tri des renvois d'un document, résolus contre orphelins.
10. **table_correspondance_renvois** — table de correspondance des renvois d'un document (type, sorte, présence, code BOI).
11. **verifier_incoherence_5465_8347** — vérification d'une incohérence unidirectionnelle de renvois entre deux documents.
12. **extraire_pieces_jointes_par_code** — extraction des pièces jointes de documents désignés par leur code.
13. **profil_age_series_bofip** — profil d'âge (fraîcheur) des documents par série.
14. **profilage_longueur_documents_bofip** — distribution de la longueur des documents.
15. **choisir_representant_par_type** — sélection d'un document représentatif par type (échantillon de commodité).
16. **verifier_constat_par_type** — passage de l'exemple à la mesure : indicateurs de structure sur les cinq types mineurs.

## Quelques chiffres clés du corpus

- **6 311** documents de type Contenu dans le stock.
- Répartition par type : Commentaire **5 679** (Parent 1 447, Enfant 4 226), Autres annexes 306, Lettre Type / Modèle 201, Formulaire 84, Barème 36, Cartographie 5.
- **29** séries documentaires (la série BIC en compte 799).
- **23 128** renvois au total (environ 3,7 par document) ; **1 354** orphelins (5,9 %) : Actualité 1 071, Contenu 265, Fichier 15, Image 3.
- **564** coquilles (527 retraits, 37 transferts) : des documents sans doctrine utile.
- Fraîcheur : 62,4 % des documents publiés avant 2020.

## Reproduire les analyses

Environnement : Python 3.13 (Anaconda recommandé). Bibliothèques principales :

```
pip install pandas openpyxl matplotlib
```

Étapes :

1. Télécharger l'archive `bofip_stock_live_20260521.tgz` à la source (voir plus haut) et la placer dans `data/`.
2. Ouvrir et exécuter d'abord `01_profilage_bofip_consolide.ipynb` : il produit l'inventaire (`.csv` et `.xlsx`) que les autres notebooks réutilisent.
3. Exécuter ensuite les autres notebooks dans l'ordre souhaité.

Les chemins sont relatifs (`./data/`). Si un fichier attendu est absent, chaque notebook
signale clairement le chemin à renseigner.

## Contexte académique

Ce dépôt accompagne le mémoire déposé par ailleurs (le PDF du mémoire est archivé via la
filière de la HEG Genève). Le dépôt sert à rendre les analyses consultables et reproductibles.
