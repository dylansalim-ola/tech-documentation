---
title: Wiki Documentation
index_img: >-
  /images/wiki.jpg
author: Dylan
tags:
  - Documentation
math: true
mermaid: true
date: 2023-06-14 18:26:00
---
>Wiki Implementation

<!-- more -->
# Wiki Implementations
## Aim 
To create a centralized, general purpose documentation for all employees in SG team (current state, may be expanded to all in the future)
One stop wiki for all, wiki shouldn't include tech stuff, but links to guides (included with tags for easy searching)
### Problem to solve 
- make it searchable
- easy to use
- reduce overhead communication

## This wiki documentation may consist of 2 parts:
1. General Purpose Wiki - Includes links to Google drive, docs, who to contact, short guides (extensive tech documentations should not be included in this wiki)
2. Tech Documentation - Includes tech-only extensive documentation, frontend and backend (open to discussion whether frontend and backend need to have a separate BookStack)
## Todo
Implement a wiki page and BookStack. Define the wiki & BookStack roles and rules

## Details of Todo:
[ ] - POC on wiki to choose
[ ] - Try Setup, find useful plugins to include, Deploy
[ ] - Setup rules and roles in the wiki
[ ] - POC on Tech Documentation implementation/others better solutions
[ ] - Try Setup, find useful plugins to include, Deploy
[ ] - Setup rules and roles in the Tech Documentation

## Criteria for Wiki:
1. Easy to edit, easy syntax recommendation
{% asset_img "/images/pm_wiki_edit_1.png" Example 1 %}
{% asset_img "/images/pm_wiki_edit_2.png" Example 2 %}
2. Role Permission to edit or view only, allow login

## Wiki Recommendations
1. [MediaWiki](https://www.mediawiki.org/wiki/MediaWiki)
Example: [Wikipedia](https://www.wikipedia.org/)
Tech Stack: PHP
2. [PmWiki](https://www.pmwiki.org/wiki/PmWiki/PmWiki)
Tech Stack: PHP
3. [DocuWiki] (https://www.dokuwiki.org/dokuwiki)
Example: 
Tech Stack: PHP
4. [Wiki.js](https://docs.requarks.io/install/config)
Tech Stack: NodeJS


## Criteria for Tech Documentation:
1. All users can create new books
2. All users can comment on existing book
3. Login feature to disable outsider to enter
   
## Tech Documentation Recommendations
1. BookStack
Example: [BookStack Demo](https://demo.bookstackapp.com/)
[Language Setup Guide](https://www.bookstackapp.com/docs/admin/language-config/)
1. [Hexo](https://hexo.io/) - Disadvantage (it is public and requires minor coding)
Example: [here](https://dylansalim-ola.github.io/tech-documentation/)
[repo](https://github.com/dylansalim-ola/tech-documentation/)

## Open for discussion
Links:
https://geekflare.com/self-hosted-wiki-software/