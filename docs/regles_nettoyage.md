# Documentation des règles de nettoyage

## 1. Présentation

Ce document décrit les anomalies identifiées lors de l'audit du dataset Sample Superstore,
les traitements appliqués et les décisions prises pour préserver l'intégrité des données.

## 2. Règles de nettoyage appliquées

| Anomalie | Traitement | Décision |
|---|---|---|
| Espaces au début et à la fin des noms de produits | Suppression avec strip() | Appliqué |
| Espaces multiples dans les noms de produits | Normalisation des espaces | Appliqué |
| Types incorrects des dates | Conversion en datetime | Appliqué |
| Type incorrect de Postal Code | Conversion en chaîne de caractères | Appliqué |

## 3. Anomalies conservées et documentées

| Anomalie | Décision | Justification |
|---|---|---|
| Doublon métier suspect | Conservation des deux lignes | Absence de preuve suffisante pour supprimer une ligne |
| Product ID associés à plusieurs noms | Conservation | Absence de référentiel produit fiable |
| Product Name associés à plusieurs IDs | Conservation | Plusieurs références peuvent correspondre à des variantes |
| Valeurs extrêmes de Sales et Profit | Conservation | Elles peuvent représenter des transactions commerciales réelles |
| Profits négatifs | Conservation | Ils représentent des pertes commerciales possibles |

## 4. Contrôles après nettoyage

Les contrôles réalisés ont notamment confirmé :

- 9 994 lignes conservées.
- 21 colonnes conservées.
- Aucune valeur manquante.
- Aucun doublon exact.
- Aucune date d'expédition antérieure à la date de commande.
- Aucun identifiant Row ID dupliqué.
- Aucune quantité nulle ou négative.

## 5. Résultat

Le dataset nettoyé a été exporté dans :

`data/processed/superstore_cleaned.csv`

Une relecture du fichier exporté a permis de vérifier la conservation des dimensions,
des colonnes et des valeurs du DataFrame nettoyé.
