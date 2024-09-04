---
title: PHP Check log
index_img: >-
  /images/h5_flutter_web/thumbnail.png
author: Dylan
tags:
  - PHP
math: true
mermaid: true
date: 2024-09-04 16:27:00
---
## PHP Check log
1. Check & verify supervisor config name
```
supervisorctl status | grep -i "php_activity"
``` 
2. Cd into the conf folder
```
cdconf
```
NOTE: cdconf is an alias to `/etc/supervisor/conf.d`
3. List out all the config info of the cmd task to log
```
cat php_activity.cmd.pt_pay_welfare.conf
```

Example conf:
```
[program:php_activity.cmd.pt_pay_welfare]
directory = /home/webroot/olachat/pta-activity/12
command = php /home/webroot/olachat/pta-activity/12/cli.php pt_pay_welfare
autostart = true
autorestart = true
startsecs = 10
stdout_logfile = /home/ecs-user/log/php_activity/php_activity.cmd.pt_pay_welfare.stdout.log
stdout_logfile_backups = 10
stdout_capture_maxbytes = 1MB
stdout_logfile_maxbytes = 20MB
redirect_stderr = true
stderr_logfile = /home/ecs-user/log/php_activity/php_activity.cmd.pt_pay_welfare.stderr.log
stderr_logfile_backups = 10
stderr_capture_maxbytes = 1MB
stderr_logfile_maxbytes = 1MB
user = ecs-user
```
Copy and directory name

4. Cd into the directory path
```
cd /home/webroot/olachat/pta-activity/12
```

5. Tail log from the cache folder
```
tail -f cache/log/web_debug_2024-09-04.log | grep "kanfjdks"
```


