# Analyse et nettoyage d'un jeu de données de ventes

## 1. Présentation du projet

Ce projet porte sur l'audit, le nettoyage et l'analyse exploratoire
d'un jeu de données transactionnelles de vente au détail en ligne.

L'objectif est de transformer des données brutes en jeux de données
fiables, documentés et exploitables pour l'analyse décisionnelle.

## 2. Source des données

- Dataset : Online Retail
- Source : UCI Machine Learning Repository
- Période couverte : décembre 2010 à décembre 2011
- Nombre de lignes initial : 541 909
- Nombre de colonnes initial : 8

Les données décrivent des transactions d'un détaillant en ligne
britannique, avec notamment les factures, les produits, les quantités,
les prix, les dates et les pays.

## 3. Technologies utilisées

- Python
- pandas
- NumPy
- Matplotlib
- Jupyter Notebook
- openpyxl

## 4. Structure du projet

```text
sales-data-analysis/
├── data/
│   ├── raw/
│   │   └── Online Retail.xlsx
│   └── processed/
│       ├── final_sales_df.csv
│       ├── final_commercial_df.csv
│       ├── final_sales_standard_df.csv
│       ├── free_lines_df.csv
│       └── potential_movements_df.csv
├── notebooks/
│   └── 01_audit_qualite.ipynb
├── reports/
│   ├── figures/
│   │   ├── temporal_analysis/
│   │   ├── product_analysis/
│   │   ├── customer_analysis/
│   │   └── geographic_analysis/
│   └── tables/
├── README.md
└── requirements.txt
```

## 5. Méthodologie

Le travail a été organisé en plusieurs étapes :

1. Chargement et inspection des données.
2. Audit de qualité : valeurs manquantes, doublons,
   incohérences et valeurs atypiques.
3. Traitement des descriptions manquantes lorsque la correspondance
   avec le code produit était suffisamment fiable.
4. Analyse des quantités, prix, factures et codes produits.
5. Identification des opérations non commerciales potentielles.
6. Classification des transactions.
7. Construction des jeux de données analytiques.
8. Analyses temporelles, produits, clients et géographie.
9. Visualisation et export des résultats.
10. Vérification de l'intégrité des fichiers exportés.

## 6. Principales décisions de nettoyage

- Les CustomerID manquants ont été conservés : leur absence ne
  justifie pas la suppression d'une transaction.
- Les descriptions manquantes ont été récupérées uniquement lorsque
  la correspondance avec le code produit était suffisamment fiable.
- Les doublons exacts ont été identifiés, mais aucune suppression
  automatique n'a été appliquée sans justification métier.
- Les factures d'annulation identifiées par le préfixe C ont été
  distinguées des ventes standard.
- Les ajustements et opérations manuelles ont été isolés.
- Les lignes gratuites ont été conservées dans un dataset dédié.
- Les mouvements non commerciaux potentiels ont été isolés sans
  les présenter comme des pertes comptables avérées.
- La cohérence entre Quantity, UnitPrice et LineTotal a été vérifiée.

## 7. Jeux de données produits

| Fichier | Description | Nombre de lignes |
|---|---|---:|
| final_sales_df.csv | Données commerciales consolidées | 532 618 |
| final_commercial_df.csv | Périmètre commercial après exclusions opérationnelles | 530 437 |
| final_sales_standard_df.csv | Ventes standard utilisées pour les analyses | 527 935 |
| free_lines_df.csv | Lignes gratuites ou sans montant | 1 166 |
| potential_movements_df.csv | Mouvements non commerciaux potentiels | 1 336 |

Les exports sont disponibles au format CSV encodé en UTF-8 avec BOM.

## 8. Résultats principaux

### Ventes standard

- Nombre de lignes : 527 935
- Nombre de factures : 19 778
- Chiffre d'affaires : 10 279 232,92 £
- Quantité vendue : 5 577 280

### Analyse temporelle

Le chiffre d'affaires atteint son niveau mensuel le plus élevé
en novembre 2011, avec 1 458 895,53 £.

Décembre 2011 est incomplet dans le jeu de données, qui s'arrête
au 9 décembre 2011.

### Analyse géographique

Le Royaume-Uni représente environ 85,12 % du chiffre d'affaires.
Les six premiers pays représentent environ 95,71 % du chiffre
d'affaires total.

### Analyse clients

4 334 clients disposent d'un identifiant exploitable dans le
périmètre des ventes standard.

Le chiffre d'affaires associé aux lignes sans CustomerID est
conservé séparément dans les analyses de couverture client.

### Analyse produits

Les classements par chiffre d'affaires et par quantité ont été
étudiés séparément. Une transaction exceptionnelle concernant
le produit 23843 a été identifiée et documentée ; elle n'a pas
été supprimée automatiquement.

## 9. Visualisations

Les graphiques sont disponibles dans `reports/figures/`.

Les analyses comprennent :

- Évolution mensuelle du chiffre d'affaires.
- Top 10 des produits par chiffre d'affaires.
- Top 10 des produits par quantité.
- Top 10 des clients par chiffre d'affaires.
- Analyse Pareto du chiffre d'affaires par pays.

Chaque graphique est sauvegardé en PNG, SVG et PDF.

## 10. Installation et exécution

Cloner ou télécharger le projet, puis installer les dépendances :

```bash
pip install -r requirements.txt
```

Placer le fichier source `Online Retail.xlsx` dans `data/raw/`.

Ouvrir ensuite le notebook :

```bash
jupyter notebook
```

Exécuter `notebooks/01_audit_qualite.ipynb` dans l'ordre.

Les chemins du notebook sont relatifs au dossier `notebooks`.

## 11. Limites et précautions d'interprétation

- Les identifiants clients manquants limitent l'analyse individuelle
  de la clientèle.
- Certaines opérations atypiques ne peuvent pas être interprétées
  avec certitude à partir des seules données disponibles.
- Les mouvements non commerciaux potentiels sont des classifications
  heuristiques et ne constituent pas des preuves comptables.
- La période de décembre 2011 est partielle.
- Les résultats décrivent le jeu de données observé et ne démontrent
  pas de relations causales.

## 12. Conclusion

Ce projet fournit un processus documenté d'audit, de nettoyage,
de classification et d'analyse de données transactionnelles.

Les jeux de données exportés distinguent les ventes standard,
les opérations commerciales élargies et certains mouvements
spécifiques afin de préserver la traçabilité des décisions.
