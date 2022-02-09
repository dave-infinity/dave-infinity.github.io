---
id: 511
title: 'django setup with virtualenv &#038; PyCharm'
date: '2015-08-25T15:47:48+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=511'
permalink: /2015/08/django-setup-with-virtualenv-pycharm/
categories:
    - Uncategorised
tags:
    - django
    - pycharm
    - virtualenv
---

### Setting up my django development (basic).

The following steps assuming that Python is installed.

1. **Setup a repository on Bitbucket:** Ensure my development machine has access via [SSH keys](http://www.davegernon.co.uk/techblog/setup-ssh-access-on-bitbucket-for-a-machine/)
2. ****Install pip on development machine:**** <https://pip.pypa.io/en/stable/installing.html>:  
    To install pip, securely download [get-pip.py](https://bootstrap.pypa.io/get-pip.py)  
    Then run the following (which may require administrator access): <div class="highlight-python"><div class="highlight">```
    $[sudo] python get-pip.py
    ```
    
    </div></div>
3. ****Install virtualenv on the development machine:**** <https://virtualenv.pypa.io/en/latest/installation.html>```
    $ [sudo] pip install virtualenv
    ```
4. **Create a working directory for the project:**```
    $mkdir /path/to/project/root
    ```
5. **Create the virtual environment to work from:**```
    $virtualenv /path/to/project/root/env
    ```
6. **Activate the virtual environment:**```
    $source /path/to/project/root/env/bin/activate
    ```
7. **Install mysql-python:**```
    <pre class="default prettyprint prettyprinted">```
    <span class="pln">(env)$[sudo]apt</span><span class="pun">-</span><span class="kwd">get</span><span class="pln"> install python</span><span class="pun">-</span><span class="pln">dev libmysqlclient</span><span class="pun">-</span><span class="pln">dev
    </span>
    ``````
    <span class="pln">
    (env)$pip install </span><span class="typ">MySQL</span><span class="pun">-</span><span class="pln">python</span>
    ```
    ```
8. **Install django 1.7:**```
    (env)$pip install django==1.7
    ```
    
    exit the virtualenv for now by:
    
    ```
    (env)$ deactivate
    ```
9. **Install pycharm to manage the project from a GUI:**  
    First install java: ```
    $ sudo add-apt-repository ppa:webupd8team/java
    $ sudo apt-get update
    $ sudo apt-get install oracle-java8-installer
    $ sudo apt-get install oracle-java8-set-default
    ```
    
    Next install pycharm:
    
    Download from [https://www.jetbrains.com/pycharm/download/  ](https://www.jetbrains.com/pycharm/download/)or from a directory outside of your project directory:
    
    ```
    $ wget http://download.jetbrains.com/python/pycharm-community-4.5.3.tar.gz
    ```
    
    change to that directory and :
    
    ```
    $ tar -xvf pycharm-community-4.5.3.tar.gz
    ```
    
    now to launch pycharm:
    
    ```
    $ ./pycharm-community-4.5.3/bin/pycharm.sh
    ```

Django 1.7, mysql-python and the pycharm editor should now be ready to use!

Next: Setting up the itstock django project <http://www.davegernon.co.uk/techblog/initial-django-setup-for-itstock-project/>