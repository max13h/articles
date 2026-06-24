---
title: "Building an Obsidian plugin that already existed"
description: "I spent two weeks building an Obsidian WebDAV sync plugin from scratch, only to discover mid-April that the exact same plugin had been published to the marketplace while I was coding. Here is what I learned from it."
author: "Maxime Hmae"
pubDate: "2026-05-25"
slug: "building_an_obsidian_plugin_that_already_existed"
translationSlug: "construire_un_plugin_obsidian_qui_existait_deja"
---

I spent two weeks coding a plugin from scratch. I planned the architecture, built the sync logic, handled edge cases, and wrote everything myself. Then one afternoon in mid-April, while checking the Obsidian plugin marketplace, I found my own project already published by someone else.

I built [obsidian-webdav-sync](https://github.com/max13h/obsidian-webdav-sync) without realizing that another plugin with the same name, [obsidian-webdav-sync](https://github.com/hesprs/obsidian-webdav-sync), already existed.

## The context

I use Obsidian as my main note-taking tool. For syncing my vault across devices, I had been relying on the WebDAV protocol - a solid, open standard that lets you mount remote storage over HTTP. My setup worked, but it ran through [remotely-save](https://github.com/remotely-save/remotely-save), a plugin that supports WebDAV among many other backends but has grown bloated over time and is unmaintained. At some point, I decided I wanted a proper, dedicated WebDAV plugin. Something focused, minimal, and actively developed.

At the beginning of March, I searched the Obsidian plugin marketplace for a WebDAV sync plugin. Nothing came up. There were a few cloud-specific options, some community workarounds, but nothing that addressed WebDAV directly and cleanly. I took that as a green light.

## Work on the project

I started with the architecture. WebDAV sync in a plugin context isn't trivial: you need to handle file diffing, conflict resolution, and the quirks of the Obsidian API - all while making the plugin feel lightweight and non-intrusive.

I designed the engine with the core sync logic, wired up the WebDAV client, built the UI, and started testing against my own server. The plugin was taking shape.

The work was not done in one intense two-week sprint. It was built little by little over a month and a half, usually in two-hour sessions after work. I would define how a feature should behave, work through it with the help of an AI assistant, iterate on the implementation, then return a few days later to continue with the next part.

## The discovery

In mid-April, about six weeks after I had started, I went back to the marketplace. Not to search for alternatives - I already "knew" there were none - but just to confirm, as a final sanity check before I prepared the submission.

There it was. [`obsidian-webdav-sync`](https://github.com/hesprs/obsidian-webdav-sync), published in the Obsidian community plugins. A WebDAV sync plugin. The same name I had given my own project. Published while I was building mine.

I sat with that for a moment.

## What went wrong

The mistake was not that I built something. The mistake was that I checked once, only into the Obsidian marketplace, not on Github or Gitlab.

The Obsidian plugin ecosystem changes quickly. New plugins appear all the time, so checking once in March does not mean the same result will still be true in April or May.

I should have checked again regularly, but also on the web for unpublished options. Especially before spending a lot of time on the project. A quick search every few weeks would have saved me two weeks of unnecessary work. It takes only a minute, but skipping it turned out to be costly.

## What I keep from this

My plugin still exists at [github.com/max13h/obsidian-webdav-sync](https://github.com/max13h/obsidian-webdav-sync). The code is there. The architecture decisions I made are mine, and I learned from making them. Two weeks of coding is never entirely wasted - I now understand the Obsidian plugin API better, I thought carefully about sync logic, and I shipped something that works.

The plugin is structured around a classify-then-execute sync engine. On each run, it gathers local files from the vault and remote files from the WebDAV server, then compares both against a persisted state file that records the last known modification time for each tracked path. Every file is classified into one of six actions - upload, download, conflict, delete-local, delete-remote, or skip - and executed sequentially. A separate scheduler handles periodic sync, and the UI is minimal: a status bar item and a ribbon indicator that reflect whether a sync is in progress or has failed.

The plugin that beat me to it is a significantly more complete implementation. It separates planning from execution: it first builds a full task graph of what needs to happen, lets the user review it, then runs tasks concurrently in optimized groups - with configurable throughput limits and automatic retry on transient errors. It adds end-to-end encryption, both file content and filenames on the remote. It ships with internationalization in three languages, and a cancellable sync that can ask for confirmation before auto-deleting local files. It is, in short, the plugin I was building toward, already finished.

But the lesson is clear: **validate your assumptions continuously, not just at the start**. Markets change. Repositories get merged. Plugins get published. The ecosystem you surveyed at the beginning of a project is not the one you are shipping into at the end.

Before building, check. Then check again halfway through. Then check again before you ship.
