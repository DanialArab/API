This repo documents my understanding of creating an API with Python|Django|MySQL|Django REST framework

Here are my notes from the course
<a href="https://www.udemy.com/course/create-an-api-with-python-django-mysql-rest-framework/?utm_source=adwords&utm_medium=udemyads&utm_campaign=Webindex_Catchall_la.EN_cc.CA&utm_term=_._ag_119831896715_._ad_533102824920_._kw__._de_c_._dm__._pl__._ti_dsa-391662294458_._li_9001493_._pd__._&matchtype=&gclid=Cj0KCQjw2qKmBhCfARIsAFy8buI9wR0ASlew2MNXtYjaTOXJscaSTUnA7m9p8ZDZPv0hfpzJl1gwHLUaAiSEEALw_wcB">Create an API with Python | Django | MySQL | REST Framework</a>


The structure of my notes is as follows:

1. [Installations](#1)
2. [Craeting a new django project](#2)
3. [Creating a new django app and CORS configuration](#3)
4. [Registering applications with django](#4)
5. [Setting up MySQL Database server to be able to interact with django application](#5)
6. [Creating a model and serializer](#6)
  


![](https://github.com/DanialArab/images/blob/main/API/course%20detail.png)

<a name="1"></a>
## Installations

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

<a name="2"></a>
## Craeting a new django project

    django-admin startproject worldCountries . 

some notes on the files in my project directory:

1. __init__.py ----> is an empty file that tells python that this directory should be considered a python package 
2. asgi.py ----> an entry-point for ASGI-compatible web servers to serve my project 
3. settings.py ----> settings/configuration for this django project 
4. urls.py ----> contains url declaration for this django projct, contains the list of routes for urls for my application 
5. wsgi.py ----> an entry-point for WSGI-compatible web servers to serve my project 
6. manage.py ----> is a command line utility that lets me interact with the django project in various ways 


<a name="3"></a>
## Creating a new django app and CORS configuration:

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

<a name="4"></a>
## Registering applications with django 

in the settings.py file and in the INSTALLED_APPS, I add the followings:

    'rest_framework',
    'countries.apps.CountriesConfig',
    'corsheaders',
    

I also need to add the middleware class in the MIDDLEWARE: 

    'corsheaders.CorsMiddleware',

A middleware is a framework of hooks into django's request/response processing. It is a light, low-level 'plugin' system for globally altering django's input or output. Each middleware component is responsible for doing some specific function. For example, django includes a middleware component, AuthenticationMiddleware, that associates users with requests using sessions. 

<a name="5"></a>
## Setting up MySQL Database server to be able to interact with django application 

![](https://github.com/DanialArab/images/blob/main/API/mysql%20workbench.png)

+ we need to create a new database in the MySQL server where django can create tables
+ we also need to create a new database user with standard authentication and some permission that we use to interact with our django application.
+ we need to install the mysqlclient, a database adapter, which enables the MySQL database to communicate with our django application (https://pypi.org/project/mysqlclient/):

    pip install mysqlclient

+ Django, by default, is prepacked with a default database sqlite, we need to change it to MySQL database. So, we need to set up the database configuration in the settings.py file:

      DATABASES = {
          'default': {
              'ENGINE': 'django.db.backends.mysql',
              'NAME': 'countriesdb',
              'USER': 'root',
              'PASSWORD': 'mypassword',
              'HOST': '127.0.0.1',
              'PORT': '3306'
          }
      }

Applying the initial migration

+  Migrations are django ways to propagate changes we make in our models into our database schema
+  the changes may include adding a field, deleting a model, etc.
+  a model is a class that represents a table or collection in a database
+  we can think of migration as a version control system for our database schema
+  migration files for each app lives inside a migrations directory inside that particular app
+  migrations are designed to be mostly automatic but it is good to know when to make a migration and also when to run a migration
+  there are several commands we use to interact with migrations and django is handling database schema:

      + migrate ---> which is responsible for applying and un-applying migrations
   
      + makemigrations ---> which is responsible for creating new migrations based on the changes we have made to our models
   
      + sqlmigrate ---> which displays the SQL statements for a migration
   
      + showmigrations ---> which lists a project's migrations and their status 

+ to run the initial migration that django craetes for us

      python3 manage.py migrate

which gives me back

    Operations to perform:
    Apply all migrations: admin, auth, contenttypes, sessions
    Running migrations:
    Applying contenttypes.0001_initial... OK
    Applying auth.0001_initial... OK
    Applying admin.0001_initial... OK
    Applying admin.0002_logentry_remove_auto_add... OK
    Applying admin.0003_logentry_add_action_flag_choices... OK
    Applying contenttypes.0002_remove_content_type_name... OK
    Applying auth.0002_alter_permission_name_max_length... OK
    Applying auth.0003_alter_user_email_max_length... OK
    Applying auth.0004_alter_user_username_opts... OK
    Applying auth.0005_alter_user_last_login_null... OK
    Applying auth.0006_require_contenttypes_0002... OK
    Applying auth.0007_alter_validators_add_error_messages... OK
    Applying auth.0008_alter_user_username_max_length... OK
    Applying auth.0009_alter_user_last_name_max_length... OK
    Applying auth.0010_alter_group_name_max_length... OK
    Applying auth.0011_update_proxy_permissions... OK
    Applying auth.0012_alter_user_first_name_max_length... OK
    Applying sessions.0001_initial... OK

<a name="2"></a>
## Creating a model and serializer 

Creating a Django model 


