This repo documents my understanding of creating an API with Python|Django|MySQL|Django REST framework

Here are my notes from the course
<a href="https://www.udemy.com/course/create-an-api-with-python-django-mysql-rest-framework/?utm_source=adwords&utm_medium=udemyads&utm_campaign=Webindex_Catchall_la.EN_cc.CA&utm_term=_._ag_119831896715_._ad_533102824920_._kw__._de_c_._dm__._pl__._ti_dsa-391662294458_._li_9001493_._pd__._&matchtype=&gclid=Cj0KCQjw2qKmBhCfARIsAFy8buI9wR0ASlew2MNXtYjaTOXJscaSTUnA7m9p8ZDZPv0hfpzJl1gwHLUaAiSEEALw_wcB">Create an API with Python | Django | MySQL | REST Framework</a>


The structure of my notes is as follows:

1. [Getting started](#1)
    1. [Installations](#2)
2. [Craeting a new django project](#3)
    1. [Creating a new django app, CORS configuration, and registering applications with django](#4)
3. [Database integration](#5)
    1. [Setting up MySQL Database server to be able to interact with django application](#6)
    2. [Applying the initial migration](#7)
4. [Creating a model and serializer](#8)
    1. [Creating a Django model ](#9)
    2. [Creating a applying new migration](#10)
    3. [Creating a serializer class](#11)
    4. [Starting and stopping a Development Server](#12)
    5. [Creating a SuperUser account](#13)
5. [Creating Views and URLs](#14)
    1. [Creating views](#15)
    2. [Mapping views to URLs](#16)
    3. [Register model with admin site](#17)
    4. [Creatig model objects](#18)
6. [Testing API](#19)
    1. [Postman](#20)
    2. [Testing API with CRUD operations](#21)
 

![](https://github.com/DanialArab/images/blob/main/API/course%20detail.png)

<a name="1"></a>
## Getting started

<a name="2"></a>
### Installations

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

<a name="3"></a>
## Creating a new django project

    django-admin startproject worldCountries . 

some notes on the files in my project directory:

1. __init__.py ----> is an empty file that tells python that this directory should be considered a python package 
2. asgi.py ----> an entry-point for ASGI-compatible web servers to serve my project 
3. settings.py ----> settings/configuration for this django project 
4. urls.py ----> contains url declaration for this django projct, contains the list of routes for urls for my application 
5. wsgi.py ----> an entry-point for WSGI-compatible web servers to serve my project 
6. manage.py ----> is a command line utility that lets me interact with the django project in various ways 


<a name="4"></a>
### Creating a new django app, CORS configuration, and registering applications with django

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


in the settings.py file and in the INSTALLED_APPS, I add the followings:

    'rest_framework',
    'countries.apps.CountriesConfig',
    'corsheaders',
    

I also need to add the middleware class in the MIDDLEWARE: 

    'corsheaders.CorsMiddleware', # This did not work I needed to modify it as 'corsheaders.middleware.CorsMiddleware', to get it work!

A middleware is a framework of hooks into django's request/response processing. It is a light, low-level 'plugin' system for globally altering django's input or output. Each middleware component is responsible for doing some specific function. For example, django includes a middleware component, AuthenticationMiddleware, that associates users with requests using sessions. 

<a name="5"></a>
## Database integration

<a name="6"></a>
### Setting up MySQL Database server to be able to interact with django application 

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

<a name="7"></a>
### Applying the initial migration

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

<a name="8"></a>
## Creating a model and serializer 

<a name="9"></a>
### Creating a Django model 

+ A model is a class that represents a table or collection in a database. A model is a class that is in the models module in django framework. 
+ I defined a name and capital attribute which will represent columns inside the database table. 

      class Countries (models.Model):
          name = models.CharField(max_length=50, blank=False, default='')
          capital = models.CharField(max_length=50, blank=False, default='')

+ Django automatically adds an auto-increment integer primary key column named id
+ I add an inner class called Meta with an ordering attribute to sort and order the records in the database by their id value in ascending order when a query is made to the database table


      class Countries (models.Model):
          name = models.CharField(max_length=50, blank=False, default='')
          capital = models.CharField(max_length=50, blank=False, default='')
      
          class Meta:
              ordering = ('id',)


<a name="10"></a>
### Creating a applying new migration 

+ Migrations are django's way of propagating changes we make to our models (adding a field, deleting a model, etc.) into our database schema. The command to create a new migration is 

    python3 manage.py makemigrations countries # if we don't supply a name after makemigrations it will use the name in the class in the model.py 

after that django automatically generates the following code in a file named 0001_initil.py in the folder migrations:

    # Generated by Django 4.2.7 on 2023-11-26 20:46
    
    from django.db import migrations, models
    
    
    class Migration(migrations.Migration):
    
        initial = True
    
        dependencies = [
        ]
    
        operations = [
            migrations.CreateModel(
                name='Countries',
                fields=[
                    ('id', models.BigAutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                    ('name', models.CharField(default='', max_length=50)),
                    ('capital', models.CharField(default='', max_length=50)),
                ],
                options={
                    'ordering': ('id',),
                },
            ),
        ]


in order to create a table in the database we have to apply migration:

    python3 manage.py migrate countries 

after applying the migration a new table is then created inside the database named after our model class, for me it will be named countries_countries

<a name="11"></a>
### Creating a serializer class

What are serializers? 

+ They allow complex data such as querysets and model instances to be converted to native Python data types that can then be easily rendered into JSON, XML, or other content types.
+ Serializers also provide deserialization, which basically allows data that has been parsed from incoming data, that has been validated, to be converted back into a complex data type.
+ The serializers in REST framework work in a similar way to django forms and ModelForm classes. 

In the countries, we create a Python file called serializers.py which contains:

    from rest_framework import serializers
    from countries.models import Countries 
    
    class CounriesSerializers(serializers.ModelSerializer):

     # class CounriesSerializers will manage serialization and deserialization from JSON. It inherits from rest_framework.serializers.ModelSerializer superclass whih automatically populates a set of fields and default validators. 
     
        class Meta:
            model = Countries
            fields = ('id', 'name', 'capital')


<a name="12"></a>
### Starting and stopping a Development Server

Django comes pre-installed with a lightweight web server which is written in Python enabling us to test our project during the development. 

    python3 manage.py runserver

we can specify the development server like

    python3 manage.py runserver 8080

SOME note:

+ that the development web server should not be used for production since it is meant to be used for development ONLY!
+ The development web server has automatic reloading which automatically restarts the web server when it detects changes in our code so we don't need to restart the server.

<a name="13"></a>
### Creating a SuperUser account

+ Every Django application has a public interface that users can interact with, it also has an administrative interface that the administrative of the application can interact with, in order to interact or access the administrative page of a django application we need to have a SuperUser account. To access the administrative page of any django application in the address bar after the port number we do a slash and then a word admin like

      http://127.0.0.1:8080/admin

this gives me access to the administrative page where I need to have a SuperUser account to log in for which in the terminal I run:

    python3 manage.py createsuperuser

where gives me a couple of prompts like creating a username, entering an email, and creating a password, like:

    python3 manage.py createsuperuser
    Username (leave blank to use 'danial'):
    Email address: danial.arab@trulioo.com
    Error: Enter a valid email address.
    Email address: danial.arab@gmail.com
    Password:
    Password (again):
    Superuser created successfully.


<a name="14"></a>
## Creating Views and URLs

<a name="15"></a>
### Creating views

+ A view is a Python function or class that takes a web request and returns a web response
+ The response can be a simple HTTP response, an HTML template response, or an HTTP redirect response that redirects a user to another page. 
+ Views are used to do things like fetch objects from the database, modify those objects if needed, render forms, return HTML, and much more
+ Django has to types of views:
    + Function-based views (FBVs)
    + Class-based views (CBVs)
+ A render is a function that creates a shortcut for communicating with a web browser 
+ JsonResponse is an HttpResponse subclass that helps create a JSON-encoded response
+ JSONParser is a parser class from REST framework used to accept JSON request
+ Status is a named constant from RESR framework used to display Http response status codes from the server following a client request
+ api_view is an api wrapper from REST framework. It is used to decorate and work with function-based views. It provides functionality to enable our django application to receive Request instances in our views. Decorators can help restrict access to certain views.
+ here is my views.py:

        from django.shortcuts import render
        from django.http.response import JsonResponse
        from rest_framework.parsers import JSONParser 
        from rest_framework import status
        
        from countries.models import Countries
        from countries.serializers import CountriesSerializers 
        from rest_framework.decorators import api_view
        
        # Create your views here.
        
        @api_view(['GET', 'POST'])
        def countries_list(request):
            if request.method == 'GET':
                countries = Countries.objects.all()
        
                name = request.GET.get('name', None)
                if name is not None:
                    countries = countries.filter(name__icontains=name)
        
                countries_serializer = CountriesSerializer(countries, many=True)
                return JsonResponse(countries_serializer.data, safe=False)
                # 'safe=False' for objects serialization
        
            elif request.method == 'POST':
                countries_data = JSONParser().parse(request)
                countries_serializer = CountriesSerializer(data=countries_data)
                if countries_serializer.is_valid():
                    countries_serializer.save()
                    return JsonResponse(countries_serializer.data, status=status.HTTP_201_CREATED)
                return JsonResponse(countries_serializer.errors, status=status.HTTP_400_BAD_REQUEST)
        
        
        
        @api_view(['GET', 'PUT', 'DELETE'])
        def countries_detail(request, pk):
            try:
                countries = Countries.objects.get(pk=pk)
            except Countries.DoesNotExist:
                return JsonResponse({'message': 'The country does not exist'}, status=status.HTTP_404_NOT_FOUND)
        
            if request.method == 'GET':
                countries_serializer = CountriesSerializer(countries)
                return JsonResponse(countries_serializer.data)
        
            elif request.method == 'PUT':
                countries_data = JSONParser().parse(request)
                countries_serializer = CountriesSerializer(countries, data=countries_data)
                if countries_serializer.is_valid():
                    countries_serializer.save()
                    return JsonResponse(countries_serializer.data)
                return JsonResponse(countries_serializer.errors, status=status.HTTP_400_BAD_REQUEST)
        
            elif request.method == 'DELETE':
                countries.delete()
                return JsonResponse({'message': 'Country was deleted successfully!'}, status=status.HTTP_204_NO_CONTENT)

some notes on the views.py above:
+ GET is used to request data from a specified resource
+ POST is used to send data to a server to create a response
+ PUT is used to send data to a server to update a resource
+ DELETE method deletes the specified resource
+ try block lets me test a block of code for errors and the except block lets me handle the error 
+ django filter allows users to filter down a queryset based on a model's fields.
+ the icontains checks if either the name or the description field contains the value of search_terms. 

<a name="16"></a>
### Mapping views to URLs 

A uniform resource locator (URL), colloquially termed a web address, is a reference to a web resource that specifies its location on a computer network and a mechanism for retrieving it. A URL is a specific type of Uniform Resource Identifier, although many people use the two terms interchangeably. 

+ The path function is contained with the django.urls module within the django project code base. path is used for routing URLs to the appropriate view functions within a django application using the URL dispatcher.
+ URLconf is a set of patterns that django tries to match with the requested URL to find the correct view. A view in django is a python function that accepts a web request and delivers a web response. In django, a request is touted through urls.py and then to the corresponding function in views.py.
+ Each view needs to be mapped to the corresponding URL pattern, which is done using a Python module called URLconf
+ URLConf is a set of patterns that django tries to match with the requested URL to find the correct view. A view in django is a Python function that accepts a web request and delivers a web response. In django, a request is routed through urls.py and then to the corresponding function in views.py.
+ Every URLConf module must contain a variable urlpatterns which is a set of URL patterns to be matched against the requested URL. In my urls.py: 

        from django.urls import path
        from . import views
        
        urlpatterns = [
        
            path('api/countries', views.countries_list),
            path('api/countries/<int:pk>', views.countries_detail)
        
        ]

also in my urls.py file inside the worldCountries project:

        from django.contrib import admin
        from django.urls import path, include 
        
        urlpatterns = [
            path('admin/', admin.site.urls),
            path('', include('countries.urls')), 
        ]


<a name="17"></a>
### Register model with admin site 

        in the admin.py file:
        
        from django.contrib import admin
        from .models import Countries 
        # Register your models here.
        
        admin.site.register(Countries)


<a name="18"></a>
### Creatig model objects 

+ Objects are records inside a database table. I want to interact with the model from the admin site of the application.
+ django automatically creates an id field behind the scene.
+ inside my models.py file:

        from django.db import models
        
        # Create your models here.
        
        
        class Countries (models.Model):
            name = models.CharField(max_length=50, blank=False, default='')
            capital = models.CharField(max_length=50, blank=False, default='')
        
            def __str__(self):
                return self.name 
        
            class Meta:
                ordering = ('id',)

+ some notes:
    + __str__ method is a string representation of the object
    + self keyword represents the instance of the class. It allows the attributes and methods of the class to be accessed. 


<a name="19"></a>
## Testing API

<a name="20"></a>
### Postman

Postman is an API platform for developers to design, build, test, and iterate their APIs. 

<a name="21"></a>
### Testing API with CRUD operations

When we are building APIs, we want our models to provide 4 basic types of functionalities. The model must be able to Create, Read, Update, and Delete (CRUD) resources. 

Before interacting with Postman to test the API, I need to make sure that my development server is up and running. 

![](https://github.com/DanialArab/images/blob/main/API/postman_testing_API.png)

It is always a good idea to keep an eye on the console for the development server as it displays interaction with the application. Like my tmux terminal is:

        [27/Nov/2023 05:26:42] "GET /static/admin/js/prepopulate_ini│(base) danial@LYVR-G6423233FB:/mnt/c/Usert.js HTTP/1.1" 304 0                                        │s/danial.arab/Downloads$
        [27/Nov/2023 05:26:42] "GET /static/admin/js/theme.js HTTP/1│
        .1" 304 0                                                   │
        [27/Nov/2023 05:26:42] "GET /static/admin/js/change_form.js │
        HTTP/1.1" 304 0                                             │
        [27/Nov/2023 05:26:42] "GET /static/admin/js/nav_sidebar.js │
        HTTP/1.1" 304 0                                             │
        [27/Nov/2023 05:26:44] "GET /admin/countries/countries/ HTTP│
        /1.1" 200 9305                                              │
        [27/Nov/2023 05:27:07] "GET /api/countries HTTP/1.1" 200 207│
        [27/Nov/2023 05:27:27] "DELETE /api/countries/4 HTTP/1.1" 20│
        4 48                                                        │
        [27/Nov/2023 05:27:29] "GET /admin/countries/countries/ HTTP│
        /1.1" 200 9092                                              │
        [27/Nov/2023 05:27:29] "GET /static/admin/css/base.css HTTP/│
        1.1" 304 0                                                  │
        [27/Nov/2023 05:27:29] "GET /static/admin/css/nav_sidebar.cs│
        s HTTP/1.1" 304 0                                           │
        [27/Nov/2023 05:27:29] "GET /static/admin/js/vendor/jquery/j│
        query.js HTTP/1.1" 304 0                                    │
        [27/Nov/2023 05:27:29] "GET /static/admin/css/changelists.cs│
        s HTTP/1.1" 304 0                                           │
        [27/Nov/2023 05:27:29] "GET /static/admin/css/dark_mode.css │
        HTTP/1.1" 304 0                                             │
        [27/Nov/2023 05:27:29] "GET /static/admin/css/responsive.css│
         HTTP/1.1" 304 0                                            │
        [27/Nov/2023 05:27:29] "GET /static/admin/js/admin/RelatedOb│
        jectLookups.js HTTP/1.1" 304 0                              │
        [27/Nov/2023 05:27:29] "GET /admin/jsi18n/ HTTP/1.1" 200 334│
        3                                                           │
        [27/Nov/2023 05:27:29] "GET /static/admin/js/core.js HTTP/1.│
        1" 304 0                                                    │
        [27/Nov/2023 05:27:29] "GET /static/admin/js/jquery.init.js │
        HTTP/1.1" 304 0                                             │
        [27/Nov/2023 05:27:29] "GET /static/admin/js/actions.js HTTP│
        /1.1" 304 0                                                 │
        [27/Nov/2023 05:27:29] "GET /static/admin/js/urlify.js HTTP/│
        1.1" 304 0                                                  │
        [27/Nov/2023 05:27:29] "GET /static/admin/js/prepopulate.js │
        HTTP/1.1" 304 0                                             │
        [27/Nov/2023 05:27:29] "GET /static/admin/js/vendor/xregexp/│
        xregexp.js HTTP/1.1" 304 0                                  │
        [27/Nov/2023 05:27:29] "GET /static/admin/js/theme.js HTTP/1│
        .1" 304 0                                                   │
        [27/Nov/2023 05:27:29] "GET /static/admin/js/nav_sidebar.js │
        HTTP/1.1" 304 0                                             │
        [27/Nov/2023 05:27:29] "GET /static/admin/js/filters.js HTTP│
        /1.1" 304 0                                                 │
                                                                    │
        [0] 0:bash*                                                         
