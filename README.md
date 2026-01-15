# Migration de NHibernate vers Entity Framework 5 (Octobre 2012)

Ce document illustre une **architecture applicative ASP.NET souple et évolutive**
et montre comment remplacer l’ORM **NHibernate** par **Entity Framework 5**
sans modifier la couche applicative.

📄 Le PDF du document est disponible ici : https://stahe.github.io/ef5cf-oct-2012/ef5cf-oct-2012.pdf  
🌐 Le site associé est accessible à l’URL : https://stahe.github.io/ef5cf-oct-2012/

---

## Contexte

**Entity Framework** est un ORM (Object Relational Mapper) initialement créé par Microsoft
et devenu open source en juillet 2012.

Dans un cours ASP.NET, ce document s’appuie sur une architecture en couches
permettant de faire évoluer les technologies (ORM, SGBD) sans impacter l’application.

---

## Architecture générale

Le schéma ci-dessous présente l’architecture utilisée dans l’application :

![Architecture ASP.NET avec NHibernate et Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/architecture.png)

### Description des couches

- **Application ASP.NET**  
  Couche de présentation et de logique applicative.

- **DAO (Data Access Objects)**  
  Interface d’accès aux données utilisée par l’application.

- **ORM (NHibernate / Entity Framework)**  
  Responsable de la génération du SQL et de la communication avec ADO.NET.

- **ADO.NET**  
  Connecteur vers le SGBD.

- **SGBD**  
  Système de gestion de base de données.

- **Spring.NET**  
  Assure l’intégration des couches et l’injection des dépendances.

---

## Pourquoi utiliser un ORM ?

Relier directement la couche DAO à ADO.NET rend l’application dépendante du SGBD :

- différences de types de données ;
- stratégies de génération des clés primaires ;
- SQL propriétaire ;
- bibliothèques spécifiques à un SGBD.

Avec un ORM, changer de SGBD revient essentiellement à **changer la configuration**
de l’ORM. La couche DAO reste inchangée.

---

## Rôle de Spring.NET

Spring.NET permet :

- à l’application ASP.NET d’obtenir une référence vers la couche DAO ;
- de créer cette couche à partir d’un fichier de configuration ;
- de remplacer une implémentation DAO par une autre **sans modifier le code**,
  tant que l’interface reste identique.

---

## Objectif du document

Démontrer concrètement que l’architecture :

- est **résistante aux changements de SGBD** ;
- est **résistante aux changements d’ORM** ;
- permet de remplacer **NHibernate par Entity Framework 5**
  sans modifier la couche applicative ASP.NET.

---

## Démarche suivie

La migration est réalisée en plusieurs étapes :

1. Découverte de **Entity Framework 5** avec plusieurs SGBD ;
2. Construction d’une nouvelle couche d’accès aux données (**DAO2**) ;
3. Connexion de l’application ASP.NET existante à cette nouvelle couche DAO.

---

## Public visé

- Développeurs ASP.NET
- Étudiants et enseignants en architecture logicielle
- Toute personne intéressée par les architectures découplées et évolutives

---

## Licence et usage

Document pédagogique destiné à l’enseignement et à la démonstration
d’architectures applicatives évolutives.
