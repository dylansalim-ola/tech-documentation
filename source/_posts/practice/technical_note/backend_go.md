---
title: Go Check log
index_img: >-
  /images/h5_flutter_web/thumbnail.png
author: Dylan
tags:
  - Go
math: true
mermaid: true
date: 2024-09-04 16:27:00
---
## pt-oversea
1. cd into supervisor conf
```
cdconf
```
OR
```
cd /etc/supervisor/conf.d
```

2. Print out your preferred conf
```
cat go_activity.http-77.conf
```

3. Get the log location and tail the log
```
less +G /home/webroot/olachat/pt-activity/77/log/http.stdout.log
```

