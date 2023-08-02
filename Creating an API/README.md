This repo documents my understanding of creating an API with Python|Django|MySQL|Django REST framework

The structure of my notes is as follows:

    conda create --name api
    conda activate api 
    cd Desktop
    mkdir countriesAPI
    python3 -m pip install --upgrade pip 
    pip install django 
    python3 -m django --version
    4.2.4

installing django rest framework to build web apis

    pip install djangorestframework
    
to see the version of the installed djangorestframework:

    pip show djangorestframework
    
    Name: djangorestframework
    Version: 3.14.0
    Summary: Web APIs for Django, made easy.
    Home-page: https://www.django-rest-framework.org/
    Author: Tom Christie
    Author-email: tom@tomchristie.com
    License: BSD
    Location: /home/danial/.local/lib/python3.10/site-packages
    Requires: django, pytz
    Required-by: 

to craete a new django project:

    django-admin startproject worldCountries . 
    
to craete a new django app:

    python3 manage.py startapp countries 

installing CORS:

+ CORS stands for **Cross Origin Resource Sharing**
+ CORS allows client applications to interface with APIs hosted on different domains
+ CORS enables us to add a set of headers that tells the web browser if it is allowed to send/receive requests from different domains
+ CORS enables requests to our django application from other origins
+ CORS can be enabled in django rest framework usign django-cors-headers package and so we need to

    pip install django-cors-headers

to configure cors we need to enter the configuration settings into the settings.py file of our django project. Only the urls listed in the whitelist are going to be allowed to communicate with our application.  

    CORS_ORIGIN_ALLOW_ALL = False
    CORS_ORIGIN_WHITELIST =('http://localhost:8080',)

if we want our application to be accessible to every url i can set:

    CORS_ORIGIN_ALLOW_ALL = True 

Registering applications with django 

Reference:
<a href="https://www.udemy.com/course/create-an-api-with-python-django-mysql-rest-framework/?utm_source=adwords&utm_medium=udemyads&utm_campaign=Webindex_Catchall_la.EN_cc.CA&utm_term=_._ag_119831896715_._ad_533102824920_._kw__._de_c_._dm__._pl__._ti_dsa-391662294458_._li_9001493_._pd__._&matchtype=&gclid=Cj0KCQjw2qKmBhCfARIsAFy8buI9wR0ASlew2MNXtYjaTOXJscaSTUnA7m9p8ZDZPv0hfpzJl1gwHLUaAiSEEALw_wcB">Create an API with Python | Django | MySQL | REST Framework</a>
