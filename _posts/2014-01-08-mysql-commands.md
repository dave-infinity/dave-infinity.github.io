---
id: 39
title: 'MySQL Commands'
date: '2014-01-08T14:09:42+00:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=39'
permalink: /2014/01/mysql-commands/
categories:
    - MySQL
---

Export:

```

mysqldump -u <em>username</em> -p <em>database_name</em> > <em>dump.sql</em>
```

Import:

```

mysql -u <em>username</em> -p <em>database_name</em> < <em>dump.sql</em>
```

Live export/duplication (note you may need to enter the password on the line for the mysql command):

```

mysql -uuser -ppassword -e 'DROP DATABASE test_db;'
mysql -uuser -ppassword -e 'CREATE DATABASE test_db;'
mysqldump -uuser -ppassword live_db | mysql -uuser -ppassword test_db;
```