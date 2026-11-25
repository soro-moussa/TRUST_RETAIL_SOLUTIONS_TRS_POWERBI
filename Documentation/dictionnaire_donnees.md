
# DICTIONNAIRE DES DONNEES

## 1. Présentation

Ce document présente la structure des données utilisées dans le projet NGELE Consulting.

## 2. Sources de données

| Fichier | Description |
|---|---:|
| Donnée_TRS_Brutes.xlsx | Données initiales du projet |
| Donnée_TRS_Traitées.xlsx | Données traitées avec Power Query |


## 3. Modélisation

Le modèle de données repose sur une architecture en étoile.

### Table de faits
- ventes_TRS_2026

### Tables de dimensions
- calendrier (Créer par une mesure DAX)

## 4. Traitement des données

- Identification des valeurs manquantes.
- Suppression des lignes vides.
- Suppression des doublons.
- Suppresion des valeurs nulles
- Correction des formats.
- Standardisation des champs.

## 5. Mesures DAX

- chiffre d'affaire Accessoire

CA Accessoire = CALCULATE([CA Total], ventes_TRS_2026[Catégorie] = "Accessoire")

- chiffre d'affaire Mobile

CA Mobile = CALCULATE([CA Total], ventes_TRS_2026[Catégorie] = "Mobile")

- chiffre d'affaire Tech

CA Tech = CALCULATE([CA Total], ventes_TRS_2026[Catégorie] = "Tech")

- chiffre d'affaire Total

CA Total = SUM(ventes_TRS_2026[Montant en $])

- Nombre de Client

Nombre Clients = DISTINCTCOUNT(ventes_TRS_2026[Client])

- Nombre de Transactions

Nombre Transactions = COUNT(ventes_TRS_2026[ID Transaction])

- Panier Moyen 

Panier Moyen = DIVIDE([CA Total],[Nombre Transactions])

- Part Chiffre D'affaire par Canal

Part Chiffre D'affaire Canal = DIVIDE([CA Total], CALCULATE([CA Total], ALL(ventes_TRS_2026[Canal])))

- Part Chiffre D'affaire par pays

Part Chiffre D'affaire pays = DIVIDE([CA Total], CALCULATE([CA Total], ALL(ventes_TRS_2026[Pays])))

- Part Chiffre D'affaire par produit

Part Chiffre D'affaire Produit = DIVIDE([CA Total], CALCULATE([CA Total], ALL(ventes_TRS_2026[Produit])))
