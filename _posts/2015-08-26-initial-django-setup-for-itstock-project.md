---
id: 525
title: 'Initial Django Setup for itstock project'
date: '2015-08-26T08:51:22+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=525'
permalink: /2015/08/initial-django-setup-for-itstock-project/
categories:
    - git
tags:
    - django
    - git
    - pycharm
---

The following steps assume you’ve completed part 1 :<http://www.davegernon.co.uk/techblog/django-setup-with-virtualenv-pycharm/>

1. **Re-activate your virtual environment (where /code/env is the location you created the virtualenv)**```
    <span class="gp">$</span> source ./code/env/bin/activate
    ```
2. **cd into the parent directory of the virtualenv (/code/) in this example:**```
    <span class="gp">(env)$</span> cd ./code
    ```
3. **Create the django project named itstock:**```
    (env)~/code/itstock$ django-admin startproject itstock
    ```
4. **Now setup Git on the ./code/itstock directory by:**```
    (env)~/code/itstock$ git init ./
    (env)~/code/itstock$ git add ./
    (env)~/code/itstock$ git commit
    ```
5. ****Next setup connection to the Bitbucket remote repository via:****  cd to the core directory of the project: ```
    (env)~/code/itstock$ cd ./itstock
    ```
6. ```
    (env)~/code/itstock/itstock$ git remote add origin git@bitbucket.org:<username>/<name of repo>
    (env)~/code/itstock/itstock$ git push -u origin --all
    (env)~/code/itstock/itstock$ git push -u origin
    ```
7. ****Integrate Bitbucket Git repo to Pycharm:****Launch pycharm and select the core directory \[~/code/itstock/itstock in my case\] as the location for the projectDownload the Bitbucket plugin from [https://plugins.jetbrains.com/plugin/?pycharm&amp;id=6207](https://plugins.jetbrains.com/plugin/?pycharm&id=6207)Within Pycharm click : File &gt; Settings &gt; Plugins &gt; Install plugin from disk…
    
    Then select the downloaded zip file and install.
    
    I got a bit lost then, you need to add the Bitbucket repo in when you want to push, maybe start with a PULL request to define that and then work from there.
8. Ensure the db is migrated:  
    Back in the terminal: ```
    (env)~/code/itstock$ python manage.py runserver <IP>:8080
    ```
9. 