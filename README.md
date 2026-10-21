# Analyse MERISE : application de simulation et d'organisation financière

Ce document regroupe le prompt de départ, les règles de gestion et le dictionnaire de données de l'application.

## Prompt final

```text
Tu travailles dans le domaine des applications de finances personnelles et d'organisation du quotidien. Ton entreprise a comme activité de concevoir et publier une application mobile utilitaire qui permet de simuler, organiser et projeter sa vie financière, 100% en local et sans collecte de données. C'est une entreprise comme YNAB, Bankin' ou Todoist. Les données ont été collectées sur : les comptes bancaires virtuels rattachés à un établissement (banque, néobanque, courtier), les opérations (dépenses, revenus, virements, récurrentes ou non, classées par catégorie), les "wallettes" qui regroupent plusieurs scénarios chiffrés composés d'éléments issus d'un catalogue de produits, les listes (d'achats avec budget, de tâches avec sous-tâches et lieux, de liens favoris), et l'agenda avec projection du solde. Inspire-toi des sites web suivants : https://www.ynab.com, https://www.bankin.com, https://todoist.com.
Ton entreprise veut appliquer MERISE pour concevoir un système d'information. Tu es chargé de la partie analyse, c'est-à-dire de collecter les besoins auprès de l'entreprise. Elle a fait appel à un étudiant en ingénierie informatique pour réaliser ce projet, tu dois lui fournir les informations nécessaires pour qu'il applique ensuite lui-même les étapes suivantes de conception et développement de la base de données.
D'abord, établis les règles de gestions des données de ton entreprise, sous la forme d'une liste à puce. Elle doit correspondre aux informations que fournit quelqu'un qui connaît le fonctionnement de l'entreprise, mais pas comment se construit un système d'information.
Ensuite, à partir de ces règles, fournis un dictionnaire de données brutes avec les colonnes suivantes, regroupées dans un tableau : signification de la donnée, type, taille en nombre de caractères ou de chiffres. Il doit y avoir entre 25 et 35 données. Il sert à fournir des informations supplémentaires sur chaque donnée (taille et type) mais sans a priori sur comment les données vont être modélisées ensuite.
Fournis donc les règles de gestion et le dictionnaire de données.
Il faut entre 25 et 35 données, et les règles doivent correspondre à ma demande
```

## Règles de gestion

### Établissements et comptes

- Un établissement a un nom et un type : banque, néobanque ou courtier.
- Un compte virtuel est rattaché à un seul établissement. Un établissement peut avoir plusieurs comptes, ou aucun si l'utilisateur ne l'a pas encore utilisé.
- Un compte a un intitulé, un solde initial et une date d'ouverture. Son solde actuel se déduit du solde initial et de ses opérations.

### Opérations et catégories

- Une opération a un libellé, un montant, une date et une nature : dépense, revenu ou virement.
- Une dépense ou un revenu concerne un seul compte. Un virement concerne deux comptes : celui qui paie et celui qui reçoit.
- Chaque dépense ou revenu est classé dans une seule catégorie. Une catégorie a un nom et un type (dépense ou revenu). Une catégorie peut regrouper beaucoup d'opérations, ou aucune.
- Une opération peut être récurrente. Elle a alors une périodicité (hebdomadaire, mensuelle, annuelle...) et, éventuellement, une date de fin. Sans date de fin, elle se répète indéfiniment.

### Catalogue, wallettes et scénarios

- Le catalogue contient des produits. Un produit a un nom, une description, un prix et une fréquence de paiement (unique, mensuel ou annuel).
- Une wallette a un nom et regroupe plusieurs scénarios chiffrés. Un scénario appartient à une seule wallette.
- Un scénario a un nom et se compose de produits du catalogue, chacun avec une quantité. Un même produit peut apparaître dans plusieurs scénarios, avec des quantités différentes.
- Le coût total d'un scénario se calcule à partir des prix et des quantités de ses produits. Il n'est pas saisi à la main.

### Listes

- Une liste a un nom et un type : achats, tâches ou liens favoris. Elle ne contient que des éléments de son type.
- Une liste d'achats a un budget. Chaque article a un libellé, un prix estimé et un indicateur "acheté ou non". Le total des articles est comparé au budget.
- Une liste de tâches contient des tâches avec un intitulé, un statut (à faire, en cours, terminée) et une échéance. Une tâche peut avoir plusieurs sous-tâches, chacune avec son libellé. Une tâche peut être associée à un lieu (nom et adresse), et un lieu peut servir à plusieurs tâches.
- Une liste de liens contient des liens favoris, chacun avec un titre et une adresse web.

### Agenda et projection

- L'agenda présente les opérations à venir, y compris les récurrences, sur une période choisie, ainsi que les échéances des tâches.
- La projection du solde d'un compte à une date future se calcule à partir de son solde actuel et des opérations prévues jusqu'à cette date. Elle n'est pas conservée.

### Confidentialité

- L'application fonctionne 100 % en local. Aucune donnée personnelle sur l'utilisateur n'est collectée : ni identité, ni e-mail, ni identifiant bancaire réel. Les comptes sont simulés.
- Les montants sont en euros, avec deux décimales.

## Dictionnaire de données

| N° | Signification de la donnée | Type | Taille |
|---|---|---|---|
| 1 | Nom de l'établissement | Alphanumérique | 50 |
| 2 | Type d'établissement (banque, néobanque, courtier) | Alphabétique | 20 |
| 3 | Intitulé du compte | Alphanumérique | 50 |
| 4 | Solde initial du compte | Numérique (2 décimales) | 10 |
| 5 | Date d'ouverture du compte | Date (JJ/MM/AAAA) | 10 |
| 6 | Libellé de l'opération | Alphanumérique | 100 |
| 7 | Montant de l'opération | Numérique (2 décimales) | 10 |
| 8 | Date de l'opération | Date (JJ/MM/AAAA) | 10 |
| 9 | Nature de l'opération (dépense, revenu, virement) | Alphabétique | 10 |
| 10 | Périodicité de l'opération récurrente | Alphabétique | 15 |
| 11 | Date de fin de la récurrence | Date (JJ/MM/AAAA) | 10 |
| 12 | Nom de la catégorie | Alphanumérique | 40 |
| 13 | Type de la catégorie (dépense ou revenu) | Alphabétique | 7 |
| 14 | Nom de la wallette | Alphanumérique | 50 |
| 15 | Nom du scénario | Alphanumérique | 50 |
| 16 | Nom du produit du catalogue | Alphanumérique | 80 |
| 17 | Description du produit | Alphanumérique | 255 |
| 18 | Prix du produit | Numérique (2 décimales) | 8 |
| 19 | Fréquence de paiement du produit (unique, mensuel, annuel) | Alphabétique | 10 |
| 20 | Quantité d'un produit dans un scénario | Numérique | 3 |
| 21 | Nom de la liste | Alphanumérique | 50 |
| 22 | Type de la liste (achats, tâches, liens) | Alphabétique | 10 |
| 23 | Budget de la liste d'achats | Numérique (2 décimales) | 8 |
| 24 | Libellé de l'article à acheter | Alphanumérique | 100 |
| 25 | Prix estimé de l'article | Numérique (2 décimales) | 8 |
| 26 | Article acheté (oui ou non) | Booléen | 1 |
| 27 | Intitulé de la tâche | Alphanumérique | 100 |
| 28 | Statut de la tâche (à faire, en cours, terminée) | Alphabétique | 10 |
| 29 | Date d'échéance de la tâche | Date (JJ/MM/AAAA) | 10 |
| 30 | Libellé de la sous-tâche | Alphanumérique | 100 |
| 31 | Nom du lieu | Alphanumérique | 60 |
| 32 | Adresse du lieu | Alphanumérique | 150 |
| 33 | Titre du lien favori | Alphanumérique | 80 |
| 34 | Adresse web du lien favori | Alphanumérique | 2048 |

Les totaux, soldes actuels et projections sont volontairement absents : ils se calculent à partir des autres données.
