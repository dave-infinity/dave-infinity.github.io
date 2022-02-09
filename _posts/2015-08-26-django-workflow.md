---
id: 539
title: 'Django Workflow'
date: '2015-08-26T12:34:55+01:00'
author: Dave
layout: post
guid: 'http://www.davegernon.co.uk/techblog/?p=539'
permalink: /2015/08/django-workflow/
categories:
    - django
tags:
    - django
    - 'django workflow'
    - 'setup django'
---

### administration:

Create the administrative user to enable logins to the /admin section of the site:

```
(env)$  python manage.py createsuperuser
```


### View &amp; URL

1. django-admin.py startapp &lt;appname&gt;
2. add the app to the projects settings.py file section: ```
    <span class="n">INSTALLED_APPS</span> <span class="o">=</span> <span class="p">(</span>
        <span class="s">'django.contrib.admin'</span><span class="p">,</span>
        <span class="s">'django.contrib.auth'</span><span class="p">,</span>
        <span class="s">'django.contrib.contenttypes'</span><span class="p">,</span>
        <span class="s">'django.contrib.sessions'</span><span class="p">,</span>
        <span class="s">'django.contrib.messages'</span><span class="p">,</span>
        <span class="s">'django.contrib.staticfiles'</span><span class="p">,</span>
        <span class="s">'<appname>'</span><span class="p">,</span>
    <span class="p">)
    </span>
    ```
3. Create a view to render: edit the &lt;appname&gt; apps views.py file: ```
    <span class="kn">from</span> <span class="nn">django.http</span> <span class="kn">import</span> <span class="n">HttpResponse</span>
    
    <span class="k">def</span> <span class="nf">index</span><span class="p">(</span><span class="n">request</span><span class="p">):</span>
        <span class="k">return</span> <span class="n">HttpResponse</span><span class="p">(</span><span class="s">"It works!"</span><span class="p">)</span>
    ```
4. Map the URL for the view: create the &lt;appname&gt; urls.py ```
    <span class="kn">from</span> <span class="nn">django.conf.urls</span> <span class="kn">import</span> <span class="n">patterns</span><span class="p">,</span> <span class="n">url</span>
    <span class="kn">from</span> <span class="nn"><appname> </span><span class="kn">import</span> <span class="n">views</span>
    
    <span class="n">urlpatterns</span> <span class="o">=</span> <span class="n">patterns</span><span class="p">(</span><span class="s">''</span><span class="p">,</span>
            <span class="n">url</span><span class="p">(</span><span class="s">r'^$'</span><span class="p">,</span> <span class="n">views</span><span class="o">.</span><span class="n">index</span><span class="p">,</span> <span class="n">name</span><span class="o">=</span><span class="s">'index'</span><span class="p">))</span>
    ```
5. Update the **project’s urls.py**  file to look for the &lt;appname&gt;’s url in the request ```
    <span class="n">urlpatterns</span> <span class="o">=</span> <span class="n">patterns</span><span class="p">(</span><span class="s">''</span><span class="p">,</span>
        <span class="c"># Examples:</span>
        <span class="c"># url(r'^$', 'tango_with_django_project_17.views.home', name='home'),</span>
        <span class="c"># url(r'^blog/', include('blog.urls')),</span>
    
        <span class="n">url</span><span class="p">(</span><span class="s">r'^admin/'</span><span class="p">,</span> <span class="n">include</span><span class="p">(</span><span class="n">admin</span><span class="o">.</span><span class="n">site</span><span class="o">.</span><span class="n">urls</span><span class="p">)),</span>
       <strong> <span class="n">url</span><span class="p">(</span><span class="s">r'^<appname>/'</span><span class="p">,</span> <span class="n">include</span><span class="p">(</span><span class="s">'<appname>.urls'</span><span class="p">)),</span> </strong>
    <span class="p">)</span>
    ```
6. Now you can visit &lt;IP&gt;:8080/&lt;appname&gt; to see your view working (do restart the server first via:  
    python manage.py runserver &lt;IP&gt;:8080 )

### Templates

Create the directory structure for the app:

1. create a **templates** directory in the **projects** root
2. inside of the **new templates** directory create a directory matching the name of your app &lt;appname&gt;
3. inside of the **/projectdir/templates/&lt;appname&gt;/** directory create an **index.html** file

Update the project settings.py:

1. edit the **projects** settings.py file and add the following where &lt;projectname&gt; is the name of the folder that houses the entire project and contains the manage.py file: ```
    <span class="n">TEMPLATE_PATH</span> <span class="o">=</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">BASE_DIR</span><span class="p">,</span> <span class="s">'<projectname>/templates'</span><span class="p">)</span>
    ```
2. then to the same file add: ```
    <span class="n">EMPLATE_DIRS</span> <span class="o">=</span> <span class="p">(</span>
        <span class="c"># Put strings here, like "/home/html/django_templates" or "C:/www/django/templates".</span>
        <span class="c"># Always use forward slashes, even on Windows.</span>
        <span class="c"># Don't forget to use absolute paths, not relative paths.</span>
        <span class="n">TEMPLATE_PATH</span><span class="p">,</span>
    <span class="p">)</span>
    ```
3. create a template view in the **/projectdir/templates/&lt;appname&gt;/index.html file**  eg: ```
    
    <html>
    
    <head>
         <title>Print Consumable Tracking</title>
    </head>
    
    <body>
         <h1>Tracking Printer Consumable Items</h1>
         <strong>{{ boldmessage }}</strong><br />
         <a href="/rango/about/">About</a><br />
    </body>
    
    </html>
    ```
4. in the application’s views.py file add: ```
    <span class="kn">from</span> <span class="nn">django.shortcuts</span> <span class="kn">import</span> <span class="n">render</span>
    ```
    
    and update the index() to:
    
    ```
    <span class="k">def</span> <span class="nf">index</span><span class="p">(</span><span class="n">request</span><span class="p">):</span>
    
        <span class="c"># Construct a dictionary to pass to the template engine as its context.</span>
        <span class="c"># Note the key boldmessage is the same as {{ boldmessage }} in the template!</span>
        <span class="n">context_dict</span> <span class="o">=</span> <span class="p">{</span><span class="s">'boldmessage'</span><span class="p">:</span> <span class="s">"I am bold font from the context"</span><span class="p">}</span>
    
        <span class="c"># Return a rendered response to send to the client.</span>
        <span class="c"># We make use of the shortcut function to make our lives easier.</span>
        <span class="c"># Note that the first parameter is the template we wish to use.</span>
    
        <span class="k">return</span> <span class="n">render</span><span class="p">(</span><span class="n">request</span><span class="p">,</span> <span class="s">'<appname>/index.html'</span><span class="p">,</span> <span class="n">context_dict</span><span class="p">)</span>
    ```

</body></html>