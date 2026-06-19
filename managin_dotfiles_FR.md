---
title: "Gérer ses dotfiles avec un 'bare' dépôt Git"
description: "Une méthode simple et élégante pour versionner ses dotfiles sans symlinks ni outils supplémentaires"
author: "Maxime Hmae"
pubDate: "2026-05-18"
slug: "gerer-ses-dotfiles"
translationSlug: "managing-dotfiles"
---

J'ai récemment découvert une technique élégante pour gérer ses dotfiles à l'aide d'un dépôt Git nu. Pas de symlinks, pas d'outils supplémentaires — juste Git.

Le tutoriel original est disponible sur [le blog d'Atlassian](https://www.atlassian.com/git/tutorials/dotfiles). Si la différence entre un dépôt nu et un dépôt classique ne vous est pas familière, ce [thread Stack Overflow](https://stackoverflow.com/questions/5540883/whats-the-practical-difference-between-a-bare-and-non-bare-repository) l'explique très bien.

Mes propres dotfiles sont disponibles sur [github.com/max13h/dotfiles](https://github.com/max13h/dotfiles).

## Comment ça fonctionne

L'idée est de stocker un dépôt Git nu dans un dossier dédié (par exemple `~/.cfg`), et d'utiliser un alias `config` pour interagir avec lui — à la place de la commande `git` habituelle. Cela évite tout conflit avec les autres dépôts Git présents sur la machine.

Ces quatre lignes suffisent pour démarrer :

```zsh
git init --bare $HOME/.cfg
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
config config --local status.showUntrackedFiles no
echo "alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'" >> $HOME/.zshrc
```

Ensuite, il suffit d'utiliser `config` comme on utiliserait `git` pour suivre n'importe quel fichier dans `$HOME` :

```zsh
config add .vimrc
config commit -m "Add vimrc"
config push
```

C'est tout.
