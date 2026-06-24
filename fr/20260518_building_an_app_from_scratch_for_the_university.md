---
title: "Construire une app de zéro pour l'université"
description: "Je reviens sur mon premier projet à l'Université de Strasbourg, Eplouribousse. Dans cet article, je partage mon expérience sur le fonctionnement des équipes lors de la réalisation d'un projet numérique, les défis que j'ai rencontrés, ainsi que les enseignements que j'ai tirés tout au long de cette aventure"
author: "Maxime Hmae"
pubDate: "2026-02-13"
slug: "construire_une_app_de_zero_pour_l_universite"
translationSlug: "building_an_app_from_scratch_for_the_university"
---

Ce projet est arrivé au bon moment dans ma carrière. Après m'être formé au métier de développeur web via la formation _Le Wagon_ pendant six mois, et en parallèle de manière autodidacte, je n'avais jusque-là travaillé que sur des projets personnels.  
Je n'avais jamais eu l'occasion de me confronter à un projet "réel": une vraie gestion de projet, en équipe, avec des enjeux concrets, des utilisateurs finaux et une méthodologie de travail clairement définie.

Eplouribousse a été mon premier projet professionnel mené sur la durée, de la phase de développement jusqu'à la mise en production. J'y ai appris énormément de choses, aussi bien sur le plan technique qu'humain, et c'est précisément ce que je souhaite partager au travers de cet article.

## Mon arrivée sur Eplouribousse

### Le contexte

J'ai été embauché en mars 2025 et j'ai rejoint le Pôle Développement, intégration et paramétrage (DIP) de la Direction du Numérique (DNUM) de l'Université de Strasbourg.

Il s'agit d'une équipe d'environ 17 personnes, travaillant sur des projets très variés au sein de l'université, mais toujours orientés développement informatique. Le pôle reçoit des demandes provenant de différentes composantes ou partenaires de l'université. Ces demandes sont évaluées en fonction des besoins, des contraintes et des financements disponibles. Lorsqu'un projet est validé, une équipe est alors être constituée pour réaliser le projet.

Cela a été le cas pour Eplouribousse, pour lequel une équipe de quatre développeurs a été allouée.

Eplouribousse est une application web dont l'objectif est de faciliter le dédoublonnement de revues au sein d'un ensemble de bibliothèques. Concrètement, lorsque plusieurs bibliothèques proches géographiquement (au sein d'une même ville ou d'un même réseau) possèdent les mêmes collections, qu'il s'agisse de bandes dessinées _Tintin_, de magazines _Le Monde_ ou de revues plus spécialisées, Eplouribousse permet d'identifier ces doublons.
L'application aide ainsi les bibliothèques à regrouper certaines collections en un lieu unique et à supprimer les exemplaires en surplus, dans le but de libérer de l'espace de stockage, une contrainte forte dans le milieu des bibliothèques universitaires.

Il existait déjà une première version de l'application, utilisée au sein du réseau des bibliothèques de Strasbourg. Cette version avait été entièrement imaginée, conçue et développée par un bibliothécaire passionné et particulièrement inventif. Son travail a permis de démontrer la pertinence du projet et de convaincre le Ministère de l'Enseignement supérieur et de la Recherche, dans le cadre des crédits Collex et d'un projet de coopération entre l'ABES et les établissements membres de son réseau, de financer une version 2 d'Eplouribousse.

### L'équipe et l'organisation

Nous travaillions selon une méthodologie agile de type Scrum, pour laquelle j'ai bénéficié d'une formation à mon arrivée.  
L'organisation du projet reposait sur plusieurs rôles bien identifiés :

- les **parties prenantes**, qui connaissent le métier des bibliothèques, expriment les besoins fonctionnels et portent la vision métier du projet ;
- le **Product Owner (PO)**, chargé de centraliser ces besoins, de les prioriser et de les traduire en éléments compréhensibles et exploitables par l'équipe de développement ;
- les **développeurs**, en charge de la conception et de la réalisation de l'application.

L'équipe de développement était composée de quatre personnes : deux développeurs côté back-end (un senior et un junior) et deux développeurs junior côté front-end, dont je faisais partie.

Très rapidement, j'ai exprimé mon envie de ne pas me cantonner uniquement au front-end, mais aussi de participer aux aspects plus transverses et critiques du projet : back-end, authentification, cache, base de données, déploiement et architecture globale.

### La stack

La stack technique du projet se présentait de la manière suivante :

- **Front-end** en TypeScript - Vue 3 (Composition API)
  - pnpm (package manager)
  - SPA (Single Page Application)
  - Vite (front-end tooling)
  - Pinia (store)
  - Quasar (UI library)
- **Back-end** en Python - Django (REST Framework)
  - Poetry (package manager)
  - Authentification locale et via Shibboleth (connexion au CAS de l'université) avec émission de JWT
  - Architecture multi-tenant (un schéma de base de données par réseau, par exemple Strasbourg, Lille, etc.)
- **Base de données** PostgreSQL
- **Cache** Redis

## Les difficultés au fil du projet

### S'adapter à un nouvel environnement de travail

En début de projet, les premières difficultés ont surtout été liées à l'adaptation à un nouvel environnement de travail.

Intégrer l'université, découvrir son fonctionnement interne, travailler avec de nouveaux collègues et s'approprier leurs pratiques de développement a demandé un temps d'ajustement. Chaque développeur ayant ses habitudes, ses standards et sa manière d'aborder le code, il a fallu apprendre à lire, comprendre et s'inscrire dans un nouvel environnement.

### Le manque d'expérience et le doute technique

Au fil de l'avancement du projet, une autre difficulté est apparue plus clairement : mon manque d'expérience.

J'ai parfois eu du mal à organiser mon code, à juger de sa qualité ou à savoir s'il répondait réellement aux attentes du projet. Il m'arrivait également d'avoir une vision partielle de l'application dans son ensemble, ce qui rendait plus complexe l'anticipation des évolutions futures.

Sur certaines fonctionnalités, j'ai eu, a posteriori, la sensation de m'engager dans des directions qui n'étaient pas optimales, simplement par manque de recul et de compréhension globale du produit.

### Comprendre le métier et maintenir une démarche agile

La difficulté la plus structurante du projet a été la compréhension du métier et son articulation avec la méthodologie agile.

Eplouribousse étant un projet déjà existant, les user stories décrivaient souvent le fonctionnement actuel de l'application plutôt que les finalités des fonctionnalités à implémenter. Il nous arrivait de connaître précisément le _comment_, sans toujours comprendre clairement le _pourquoi_.

Dans certains cas, les user stories entraient rapidement dans des détails d'implémentation, laissant peu de place à la réflexion fonctionnelle et technique. Combiné à un vocabulaire très métier, cela rendait leur interprétation délicate et nécessitait de nombreux échanges avec le Product Owner et les parties prenantes.

Ces allers-retours ont été essentiels pour aligner la compréhension des besoins réels, mais ils ont également représenté une part importante du temps consacré au projet.

## Ce que j'ai appris

### Techniquement

Sur le plan technique, ce projet m'a appris à dépasser une logique purement fonctionnelle. Il ne s'agissait plus seulement de faire "marcher" une fonctionnalité, mais de l'intégrer dans une application existante, amenée à évoluer dans le temps.

J'ai appris à travailler sur une base de code partagée, à composer avec des choix techniques déjà en place et à questionner mes propres décisions avec davantage de recul. Avec le temps, j'ai commencé à identifier certaines limites dans des choix faits en début de projet, ce qui m'a permis de mieux comprendre les notions de compromis, de dette technique et d'amélioration continue.

### Humainement

Humainement, ce projet m'a fait prendre conscience que le développement logiciel est avant tout un travail collectif. La communication, les échanges et la compréhension mutuelle sont aussi importants que les compétences techniques.

J'ai appris à mieux expliquer mon travail, à écouter celui des autres et à accepter les retours, qu'ils soient techniques ou fonctionnels. Les nombreux échanges avec le Product Owner et les parties prenantes m'ont également montré à quel point le dialogue avec le métier est essentiel pour construire une application réellement utile.

### Sur moi-même

Ce projet m'a également beaucoup appris sur moi-même. J'y ai découvert mes limites, mes doutes, mais aussi ma capacité à progresser sur la durée.

Avec le temps, j'ai gagné en confiance et en légitimité, en acceptant de ne pas tout savoir dès le départ et en apprenant à demander de l'aide lorsque c'était nécessaire. J'ai peu à peu changé de posture, passant d'un rôle d'exécutant à celui de contributeur impliqué dans les réflexions autour du produit.

J'ai également appris à accepter la lenteur comme une contrainte normale, à comprendre qu'un projet réel n'est jamais totalement "propre", et à livrer même lorsque tout n'est pas idéal.

## La mise en production : un vrai cap

La mise en production est une étape que je savais essentielle dans le métier de développeur.
En début de projet, nous travaillions sur des machines virtuelles hébergées dans le data center de l'université. Les outils de déploiement étaient internes (tel que des scripts shell), mais suffisants pour répondre aux besoins des projet du pôle.

Nous fonctionnions avec trois environnements distincts :

- un environnement de **test**, fermé au réseau de l'université, utilisé pour des déploiements fréquents et la validation par le Product Owner
- un environnement de **pré-production**, ouvert à internet, destiné aux tests et validations par les parties prenantes
- l'environnement de **production**, destiné aux utilisateurs finaux

Ce fonctionnement a été en place pendant la majeure partie du projet. En fin d'année 2025, alors que le projet se rapprochait de sa version finale, une nouvelle infrastructure basée sur OpenShift a été mise en place au sein de l'université. Il nous a alors été proposé d'utiliser cette plateforme pour la mise en production d'Eplouribousse.

Cette nouvelle infrastructure impliquait un changement important dans notre manière de déployer l'application. Le déploiement reposait désormais sur la création d'images Docker pour le front et le back, images qui sont construites automatiquement via notre les CI respectives. Ces images sont ensuite publiées sur le registre de conteneurs Quay, afin d'être consommées par Kubernetes au sein d'OpenShift lors des déploiements.

Nous avons reproduit nos trois environnements sur cette nouvelle infrastructure, recréé les bases de données ainsi que les services Redis nécessaires au cache. La gestion technique de l'infrastructure a été assurée par une équipe dédiée, et nous avons suivi cette mise en place afin de nous familiariser avec l'architecture, les concepts et le vocabulaire associés.

Les déploiements s'appuient désormais sur des charts Helm versionnés dans un dépôt Git, ce qui apporte davantage de stabilité, de reproductibilité et de flexibilité. Cette transition m'a permis de mieux comprendre les enjeux liés au déploiement en production, ainsi que l'importance de l'infrastructure dans le cycle de vie d'une application.

## Conclusion - Ce que ce projet m'a laissé

Avec le recul, je me rends compte à quel point j'ai été chanceux de pouvoir travailler sur un projet comme Eplouribousse. À la fois complet, concret et exigeant, il m'a permis de découvrir le métier de développeur dans des conditions réelles : en équipe, sur la durée, avec des contraintes techniques, organisationnelles et humaines. Au-delà des compétences techniques, ce projet m'a appris à travailler dans un cadre structuré, à communiquer avec des profils variés. J'ai encore beaucoup de choses à apprendre, mais Eplouribousse a posé des bases solides sur lesquelles je peux désormais m'appuyer.

Je tiens également à remercier l'ensemble de l'équipe projet: développeurs, Product Owner et parties prenantes, pour leur accompagnement, leur disponibilité et la confiance qui m'a été accordée tout au long du projet. Je remercie également l'université pour l'opportunité de participer à un projet de cette ampleur, qui restera pour moi une étape fondatrice de mon parcours et un point de référence dans ma manière d'aborder les projets à venir.
