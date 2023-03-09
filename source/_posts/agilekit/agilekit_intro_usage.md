---
title: AgileKit
index_img: >-
  https://rmt.dogedoge.com/fetch/fluid/storage/hello-fluid/cover.png?w=480&fmt=webp
author: Dylan
tags:
  - AgileKit
  - Github Project
math: true
mermaid: true
sticky: 100
date: 2023-03-09 18:26:00
---
>AgileKit Docs and usage，Ticket: https://github.com/olachat/agilekit

<!-- more -->
# agilekit
Go project to organize and process github issues.

## Prerequisite
- go version 1.19

## To generate CSV file
1. Update the conf.toml
```yaml
[app]
port=5555
GithubToken="YOUR_GITHUB_TOKEN"
OrgName="olachat"
ProjectNumber=12380446
TeamName="veeka"
GithubAPIUrl="https://api.github.com/"
```
2. Generate CSV Files
a. Generate for all sprints
```bash
 make Makefile -C /Users/ola_friend/Documents/REPO/agilekit okr-all 
```

b. Generate for current sprint only
```bash
 make Makefile -C /Users/ola_friend/Documents/REPO/agilekit okr-current 
```


## To Archive old issues
1. Dry run to view the closable issues available
```bash
 make Makefile -C /Users/ola_friend/Documents/REPO/agilekit archive 
```

2. Execute close command to all closable issues <br>(WARNING: Run this cmd only when you know what you are doing)
```bash
 make Makefile -C /Users/ola_friend/Documents/REPO/agilekit archive-exec
```
