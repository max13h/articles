---
title: "Managing dotfiles with a bare Git repository"
description: "A simple and elegant way to version your dotfiles without symlinks or extra tooling"
author: "Maxime Hmae"
pubDate: "2026-05-18"
slug: "managing-dotfiles"
translationSlug: "gerer-ses-dotfiles"
---

I recently came across an elegant technique for managing dotfiles using a bare Git repository. No symlinks, no extra tooling — just Git.

The original tutorial is available on [Atlassian's blog](https://www.atlassian.com/git/tutorials/dotfiles). If you're not familiar with the difference between a bare and a non-bare repository, this [Stack Overflow thread](https://stackoverflow.com/questions/5540883/whats-the-practical-difference-between-a-bare-and-non-bare-repository) explains it well.

My own dotfiles are available at [github.com/max13h/dotfiles](https://github.com/max13h/dotfiles).

## How it works

The idea is to store a bare Git repository in a dedicated folder (e.g. `~/.cfg`), and use a `config` alias to interact with it — instead of the usual `git` command. This avoids any conflict with other Git repositories on your machine.

Run these four lines to get started:

```zsh
git init --bare $HOME/.cfg
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
config config --local status.showUntrackedFiles no
echo "alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'" >> $HOME/.zshrc
```

From there, you can track any file in your `$HOME` using `config` just like you would use `git`:

```zsh
config add .vimrc
config commit -m "Add vimrc"
config push
```

That's it.
