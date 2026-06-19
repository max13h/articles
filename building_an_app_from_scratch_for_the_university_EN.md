---
title: "Building an app from scratch for the university"
description: "I look back on my first project at the University of Strasbourg, Eplouribousse. In this article, I share my experience on how teams operate when building a digital project, the challenges I faced, and the lessons I learned throughout this adventure"
author: "Maxime Hmae"
pubDate: "2026-02-13"
slug: "building_an_app_from_scratch_for_the_university"
translationSlug: "construire_une_app_de_zero_pour_l_universite"
---

This project came at the right time in my career. After training as a web developer through the six-month _Le Wagon_ bootcamp, and simultaneously teaching myself on the side, I had only ever worked on personal projects.
I had never had the opportunity to tackle a "real" project: genuine project management, working in a team, with concrete stakes, end users, and a clearly defined work methodology.

Eplouribousse was my first professional project carried out over an extended period, from the development phase all the way to production deployment. I learned a tremendous amount, both technically and on a human level, and that is precisely what I want to share through this article.

## My arrival on Eplouribousse

### The context

I was hired in March 2025 and joined the Development, Integration and Configuration division (DIP) of the Digital Directorate (DNUM) at the University of Strasbourg.

It is a team of about 17 people, working on a wide variety of projects within the university, all centered around software development. The division receives requests from various departments or partners of the university. These requests are evaluated based on needs, constraints, and available funding. When a project is approved, a team is then assembled to carry it out.

This was the case for Eplouribousse, for which a team of four developers was allocated.

Eplouribousse is a web application whose goal is to facilitate the deduplication of journal holdings across a network of libraries. In practice, when several geographically close libraries (within the same city or the same network) hold the same collections - whether _Tintin_ comics, _Le Monde_ magazines, or more specialized journals - Eplouribousse identifies these duplicates.
The application thus helps libraries consolidate certain collections in a single location and remove surplus copies, with the aim of freeing up storage space, a significant constraint in the world of university libraries.

A first version of the application already existed, used within the Strasbourg library network. This version had been entirely imagined, designed, and developed by a passionate and particularly inventive librarian. His work demonstrated the relevance of the project and convinced the Ministry of Higher Education and Research, as part of the Collex funding program and a cooperation project between ABES and the member institutions of its network, to fund a version 2 of Eplouribousse.

### The team and organization

We worked using an agile Scrum methodology, for which I received training when I arrived.
The project organization was based on several clearly identified roles:

- the **stakeholders**, who understand the library profession, express functional needs, and carry the business vision of the project;
- the **Product Owner (PO)**, responsible for centralizing these needs, prioritizing them, and translating them into elements that are understandable and actionable by the development team;
- the **developers**, in charge of designing and building the application.

The development team was made up of four people: two back-end developers (one senior and one junior) and two junior front-end developers, of which I was one.

Very quickly, I expressed my desire not to be limited to front-end work only, but also to participate in the more cross-cutting and critical aspects of the project: back-end, authentication, caching, database, deployment, and overall architecture.

### The stack

The project's technical stack was as follows:

- **Front-end** in TypeScript - Vue 3 (Composition API)
  - pnpm (package manager)
  - SPA (Single Page Application)
  - Vite (front-end tooling)
  - Pinia (store)
  - Quasar (UI library)
- **Back-end** in Python - Django (REST Framework)
  - Poetry (package manager)
  - Local authentication and via Shibboleth (connection to the university's CAS) with JWT issuance
  - Multi-tenant architecture (one database schema per network, e.g., Strasbourg, Lille, etc.)
- **Database** PostgreSQL
- **Cache** Redis

## Challenges throughout the project

### Adapting to a new work environment

At the start of the project, the initial challenges were mainly related to adapting to a new work environment.

Joining the university, discovering how it operates internally, working with new colleagues, and getting familiar with their development practices required an adjustment period. Since every developer has their own habits, standards, and approach to code, I had to learn to read, understand, and fit into a new environment.

### Lack of experience and technical doubt

As the project progressed, another challenge became more apparent: my lack of experience.

I sometimes struggled to organize my code, to assess its quality, or to know whether it truly met the project's expectations. I also occasionally had only a partial view of the application as a whole, which made it more difficult to anticipate future developments.

On certain features, I had the feeling, in hindsight, of heading in directions that were not optimal, simply due to a lack of perspective and overall understanding of the product.

### Understanding the business domain and maintaining an agile approach

The most structurally significant challenge of the project was understanding the business domain and how it articulated with the agile methodology.

Since Eplouribousse was an already existing project, user stories often described how the current application worked rather than the goals of the features to be implemented. We sometimes knew precisely the _how_, without always clearly understanding the _why_.

In some cases, user stories quickly went into implementation details, leaving little room for functional and technical reflection. Combined with highly specialized business vocabulary, this made their interpretation delicate and required numerous exchanges with the Product Owner and stakeholders.

These back-and-forth discussions were essential to align the understanding of actual needs, but they also represented a significant portion of the time spent on the project.

## What I learned

### Technically

On the technical side, this project taught me to go beyond a purely functional mindset. It was no longer just about making a feature "work", but about integrating it into an existing application that would evolve over time.

I learned to work on a shared codebase, to work with technical choices already in place, and to question my own decisions with greater perspective. Over time, I began to identify certain limitations in choices made at the beginning of the project, which helped me better understand the concepts of trade-offs, technical debt, and continuous improvement.

### On a human level

On a human level, this project made me realize that software development is above all a collective endeavor. Communication, exchanges, and mutual understanding are just as important as technical skills.

I learned to better explain my work, to listen to others, and to accept feedback, whether technical or functional. The many exchanges with the Product Owner and stakeholders also showed me how essential dialogue with the business side is in order to build a truly useful application.

### About myself

This project also taught me a lot about myself. I discovered my limits, my doubts, but also my ability to grow over time.

Gradually, I gained confidence and legitimacy by accepting that I didn't need to know everything from the start and by learning to ask for help when necessary. I progressively shifted my posture, moving from a role of executor to that of a contributor involved in discussions about the product.

I also learned to accept slowness as a normal constraint, to understand that a real project is never completely "clean", and to deliver even when everything is not ideal.

## Going to production: a real milestone

Going to production is a step I knew was essential in the developer profession.
At the start of the project, we were working on virtual machines hosted in the university's data center. The deployment tools were internal (such as shell scripts), but sufficient to meet the needs of the division's projects.

We operated with three distinct environments:

- a **test** environment, closed to the university network, used for frequent deployments and validation by the Product Owner
- a **pre-production** environment, open to the internet, intended for testing and validation by stakeholders
- the **production** environment, intended for end users

This setup was in place for most of the project. At the end of 2025, as the project was approaching its final version, a new infrastructure based on OpenShift was set up within the university. We were then offered the opportunity to use this platform for the production deployment of Eplouribousse.

This new infrastructure entailed a significant change in how we deployed the application. Deployment was now based on creating Docker images for the front-end and back-end, which are built automatically via our respective CI pipelines. These images are then published to the Quay container registry, to be consumed by Kubernetes within OpenShift during deployments.

We reproduced our three environments on this new infrastructure, recreated the databases and the Redis services needed for caching. The technical management of the infrastructure was handled by a dedicated team, and we followed this setup in order to familiarize ourselves with the architecture, concepts, and associated vocabulary.

Deployments now rely on Helm charts versioned in a Git repository, which brings greater stability, reproducibility, and flexibility. This transition helped me better understand the challenges related to production deployment, as well as the importance of infrastructure in the lifecycle of an application.

## Conclusion - What this project left me with

Looking back, I realize how lucky I was to be able to work on a project like Eplouribousse. At once comprehensive, concrete, and demanding, it allowed me to discover the developer profession under real conditions: in a team, over an extended period, with technical, organizational, and human constraints. Beyond technical skills, this project taught me to work within a structured framework and to communicate with people of varied profiles. I still have a lot to learn, but Eplouribousse laid solid foundations on which I can now build.

I also want to thank the entire project team - developers, Product Owner, and stakeholders - for their support, their availability, and the trust that was placed in me throughout the project. I also thank the university for the opportunity to participate in a project of this scale, which will remain for me a foundational milestone in my journey and a point of reference in how I approach future projects.
