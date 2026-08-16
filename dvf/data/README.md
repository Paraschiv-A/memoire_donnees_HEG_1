# Dossier data/

Ce dossier accueille le fichier de données lu par les notebooks.

## À déposer ici

- **`dvf-2022.parquet`** : le fichier DVF 2022 au format Parquet (version consolidée
  icem7, environ 105 Mo). Il **n'est pas versionné** sur GitHub (trop volumineux) et se
  retélécharge librement depuis data.gouv.fr.

Une fois le fichier placé ici, les notebooks le lisent via le chemin relatif
`./data/dvf-2022.parquet`. Aucun autre fichier de données n'est nécessaire.
