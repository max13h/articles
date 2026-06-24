---
title: "Construire un plugin Obsidian qui existait déjà"
description: "J'ai passé deux semaines à développer un plugin de synchronisation WebDAV pour Obsidian, avant de découvrir mi-avril qu'un plugin quasiment identique avait déjà été publié pendant que je codais. Voici ce que j'en ai retenu."
author: "Maxime Hmae"
pubDate: "2026-05-25"
slug: "construire_un_plugin_obsidian_qui_existait_deja"
translationSlug: "building_an_obsidian_plugin_that_already_existed"
---

J'ai passé deux semaines à développer un plugin depuis zéro. J'ai pensé l'architecture, construit la logique de synchronisation, géré les cas particuliers et écrit tout le code moi-même. Puis un après-midi de mi-avril, en vérifiant la marketplace des plugins Obsidian, j'ai découvert que mon propre projet avait déjà été publié... par quelqu'un d'autre.

J'ai développé [obsidian-webdav-sync](https://github.com/max13h/obsidian-webdav-sync) sans me rendre compte qu'un autre plugin portant exactement le même nom, [obsidian-webdav-sync](https://github.com/hesprs/obsidian-webdav-sync), existait déjà.

## Le contexte

J'utilise Obsidian comme principal outil de prise de notes. Pour synchroniser mon vault entre mes appareils, j'utilisais le protocole WebDAV - un standard ouvert et fiable qui permet de monter un stockage distant via HTTP. Ma configuration fonctionnait, mais elle reposait sur [remotely-save](https://github.com/remotely-save/remotely-save), un plugin qui prend en charge WebDAV parmi beaucoup d'autres backends, mais qui est devenu assez lourd avec le temps et n'est plus maintenu. À un moment, j'ai décidé que je voulais un vrai plugin WebDAV dédié : quelque chose de simple, ciblé et activement développé.

Début mars, j'ai cherché un plugin de synchronisation WebDAV dans la marketplace d'Obsidian. Je n'ai rien trouvé. Il existait quelques solutions spécifiques à certains clouds et quelques solutions communautaires, mais rien qui gérait WebDAV de manière directe et propre. J'ai pris ça comme une opportunité de m'améliorer.

## Travail sur le projet

J'ai commencé par l'architecture. La synchronisation WebDAV dans le contexte d'un plugin n'est pas triviale : il faut gérer les différences de fichiers, les conflits, et les particularités de l'API Obsidian tout en gardant un plugin léger et discret.

J'ai conçu le moteur de synchronisation, connecté le client WebDAV, construit l'interface et commencé les tests sur mon propre serveur. Petit à petit, le plugin prenait forme.

Le travail ne s'est pas fait en une seule période intense de deux semaines. Le projet s'est construit petit à petit sur un mois et demi, généralement par sessions de deux heures. Je définissais le comportement attendu d'une fonctionnalité, travaillais dessus avec l'aide d'un assistant IA, itérais sur l'implémentation, puis revenais quelques jours plus tard pour continuer sur la partie suivante.

## La découverte

Mi-avril, environ six semaines après avoir commencé, je suis retourné sur la marketplace. Pas pour chercher des alternatives - j'étais déjà persuadé qu'il n'y en avait pas - mais simplement pour une dernière vérification avant de préparer la publication.

Il était là : [obsidian-webdav-sync](https://github.com/hesprs/obsidian-webdav-sync), publié dans les plugins communautaires Obsidian. Un plugin de synchronisation WebDAV. Le même nom que celui que j'avais donné à mon propre projet. Publié pendant que je développais le mien.

Je suis resté bloqué quelques instants devant ça.

## Qu'est ce que j'ai mal fait ?

L'erreur n'était pas d'avoir construit quelque chose. L'erreur, c'était d'avoir vérifié une seule fois, uniquement dans la marketplace Obsidian, et pas sur Github ou Gitlab.

L'écosystème des plugins Obsidian évolue rapidement. De nouveaux plugins apparaissent constamment, donc une recherche effectuée en mars ne garantit rien pour avril ou mai.

J'aurais dû vérifier régulièrement, mais aussi chercher sur le web des projets non publiés. Surtout avant d'investir autant de temps dans le projet. Une recherche rapide toutes les quelques semaines m'aurait évité deux semaines de travail inutile. Ça prend une minute, mais ne pas le faire m'a coûté cher.

## Ce que j'en retiens

Mon plugin existe toujours sur [github.com/max13h/obsidian-webdav-sync](https://github.com/max13h/obsidian-webdav-sync). Le code est là. Les choix d'architecture que j'ai faits sont les miens, et j'ai appris en les faisant. Deux semaines de développement ne sont jamais totalement perdues : je comprends maintenant beaucoup mieux l'API des plugins Obsidian, j'ai réfléchi sérieusement à la logique de synchronisation, et j'ai livré quelque chose qui fonctionne.

Le plugin est organisé autour d'un moteur de synchronisation basé sur une logique "classifier puis exécuter". À chaque synchronisation, il récupère les fichiers locaux du vault et les fichiers distants du serveur WebDAV, puis compare les deux avec un fichier "d'état" persistant qui stocke la dernière date de modification connue pour chaque chemin suivi. Chaque fichier est ensuite classé dans une des six actions possibles - upload, download, conflict, delete-local, delete-remote ou skip - puis exécuté séquentiellement. Un scheduler séparé gère les synchronisations périodiques, et l'interface reste minimale : un indicateur dans la barre de statut et une icône dans le ruban affichent si une synchronisation est en cours ou a échoué.

Le plugin qui m'a devancé est une implémentation beaucoup plus complète. Il sépare la planification de l'exécution : il construit d'abord un graphe complet des tâches à effectuer, permet à l'utilisateur de le relire, puis exécute les tâches en parallèle avec des groupes optimisés, des limites de débit configurables et des tentatives automatiques en cas d'erreurs temporaires. Il ajoute aussi le chiffrement de bout en bout, aussi bien pour le contenu des fichiers que pour leurs noms côté distant. Il inclut de l'internationalisation en trois langues et une synchronisation annulable capable de demander confirmation avant de supprimer automatiquement des fichiers locaux. En résumé, c'était déjà le plugin vers lequel je me dirigeais.

Mais la leçon est claire : **il faut valider la pertinence du produit en continu, pas seulement au début**. Les marchés changent. Les repos sont fusionnés. Les plugins sont publiés. L'écosystème que vous avez observé au début d'un projet n'est plus forcément celui dans lequel vous allez publier à la fin.

Avant de construire quelque chose, vérifiez. Puis revérifiez au milieu du projet. Et revérifiez encore avant de publier.
