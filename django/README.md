- [Django Cheatsheet]()  
- [Django Basics Part 1 - Components]()  
- [Django Basics Part 2 - Simple Crud App]()  

# Django Cheatsheet  

# Django Basics Part 1 - Components   

## Introduction  

* Django is a high-level python web framework 
* Encourages rapid development 
* It consists clean and pragmatic design  

## MVT Model 

Djnago is based on MVT architecture

* MODEL     
    * Represents the data/database of the application.   
    * Acts as the interface between the application and data
    * Responsible for maintaing data
* VIEW  
    * Responsible for User Interface  
    * Randers front-end of webpage what the users see on their browser.   
    * Represented by HTML/CSS/Javascript.  
* TEMPLATE   
    * Consists of static parts of the desired HTML output as well as some special syntax describing how dynamic content will be inserted.   

## Project and App   

* __PROJECT:__ A Project refers to an entire web application, for example an ecommerce website.     

* __APP:__ 
    * An App refers to a submodule of the project. For example in ecommerce website shopping cart is an app and chekout, user_information, product search, ship traking all functionalities are standalone apps. 
    * Apps are self-sufficient and not intertwined with the other apps in the project such that, in theory, you could pick it up and plop it down into another project without any modification. 
    * An app typically has its own models.py (which might actually be empty). You might think of it as a standalone python module.

## Setting up environment and Installing django   

Setting up virtualenv  

```py
virtualenv -p python3 venv
.\venv\Scripts\activate
```

Now installing django  

```shell   
pip3 install django
// installs the latest version of django  
```  

## Creating first Project  

```shell
django-admin startproject myproject 
```

File structure 

```shell  
myproject/
├── manage.py
└── myproject
    ├── asgi.py
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```  

* folder contains all the files related to project.  
* Inside there is a file `manage.py` and another directory `myproject`.  

### manage.py     

Command-line utility and for deploying, debugging, or running our web application. Usage :    

```shell   
python manage.py <command>    
```  

Some important commands :    

* `runserver` : Run server (temporary developer server) for the web application.  

```shell   
python manage.py runserver 
```  

* `migrate` :  Synchronizes the database state with the current set of models and migrations.  

```shell      
python manage.py migrate 
```  

* `makemigrations` : Creates new migrations based on the changes detected to your Apps models. Basically used for migrating models of apps only.    

```shell        
python manage.py makemigrations App_Name    
```  

* `shell` : Start the django interactive shell.  

```shell        
python manage.py shell  
```    

### myproject     

Contains all the data related to the web application.      

* __wsgi.py:__     
    * Web Server Gateway Interface can be thought of as a specification that describes how the servers interact with web applications.   
    * It is used for deploying our applications on to servers like Apache etc.     
* __asgi.py:__    
    * Asynchronous Server Gateway interface
    * Has the work similar to WSGI but this is better than the previous one as it gives better freedom in Django development. That’s why WSGI is now being increasingly replaced by ASGI.  
* **\_\_init\_\_.py**  
    * This file remains empty and is present their only to tell that this particular directory(in this case myproject) is a package.  
* __settings.py__ 
    * This file is present for adding all the applications and the middleware application present.  
    * Also, it has information about templates and databases.   
    * Overall, this is the main file of our Django web application. The code which we are currently interested are :  

```shell   
DEBUG = True
```  

for production server set it "False". 

```shell  
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```  

Add the newly created apps on the above lists. Example : 

```shell       
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp1.apps.Myapp1Config',
    'myapp2.apps.Myapp2Config',
    'myapp3.apps.Myapp3Config',
]
```  

The name of appConfig class can be found in `myapp1/apps.py`.  

* __urls.py:__    
    * This file handles all the URLs of our web application. This file has the lists of all the endpoints that we will have for our website. For example we can add url for our app as :

First import include and path lib 

```shell     
from django.urls import path, include
```  

Add the path  

```shell    
urlpatterns = [
    path('admin/', admin.site.urls),
    path('myapp1/', include('myapp1.urls')),
    path('myapp2/', include('myapp2.urls')),
    path('myapp3/', include('myapp3.urls')),
]
```  

## Creating Apps  

Create App Project inside Main Project folder where manage.py resides.    

```shell          
django-admin startapp myapp1 
``` 

Now the whole project tree looks like  this 

```shell  
├── manage.py
├── myapp1
│   ├── admin.py
│   ├── apps.py
│   ├── __init__.py
│   ├── migrations
│   │   └── __init__.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
└── myproject
    ├── asgi.py
    ├── __init__.py
    ├── __pycache__
    │   ├── __init__.cpython-36.pyc
    │   └── settings.cpython-36.pyc
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```  

Lets look at the myapp1 directory

```shell  
myapp1/
├── admin.py
├── apps.py
├── __init__.py
├── migrations
│   └── __init__.py
├── models.py
├── tests.py
└── views.py
```  

* __admin.py:__ Used for registering the models into the Django administration.   
* __apps.py:__ This file deals with the application configuration of the apps.     
* \_\_init\_\_.py : This file has the same functionality just as in the \_\_init\_\_.py file in the Django project structure. It remains empty and is present just to indicate that the specific app directory is a package.  
* __models.py__ : This file is used to write Class based Models for our Django Applications.This will be the blueprint of our database design ,relationships and attribute constraints.   
* __tests.py__ : This file contains the code that contains different test cases for the application. It is used to test the working of the application.     
* __views.py__ : This file is a crucial one, it contains all the Views(usually as classes). Views.py can be considered as a file that interacts with the client. Views are a user interface for what we see when we render a Django Web application. 

Example of view file:  

```python
from django.shortcuts import render
from django.http import HttpResponse
# Create your views here.

def index(request):
    return HttpResponse("Hello world, You're at the Myapp1 index.")
```  

* __migrations__ : The migrations directory contains all the migration data (models as sql queries form).    


## Running the Django Project  

* __Creating a urls.py file in app directory__ : Also create a file `urls.py` in `myproject/myapp1/` so we can map the rest of the URI for this app from here itself, not from the myproject's urls.py file. Exmple of urls.py file for myapp1 :    

```python   
from django.urls import path
from . import views

urlpatterns = [
        path('', views.index, name='index'),
    ]
```  

* Configurig `Settings.py`` file in project directory `myproject/myproject/`  

Add the below lines to Settings.py  


```python  
 "myapp1.apps.Myapp1Config",
``` 

Now it will look like this  

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp1.apps.Myapp1Config',
]
```   

Now add below lines on myproject/urls.py  

```python
from django.contrib import admin
from django.urls import path, include   

urlpatterns = [
    path("admin/", admin.site.urls),
    path('myapp1/', include('myapp1.urls')),  
]
``` 

Now migrate and start the server 

```python   
python manage.py migrate
python manage.py runserver  
```  

Then goto http://localhost:8000/myapp1/ 

## Some Important Commands  

**Making Migrations :**  

Migrations can be made when a new model is created in an app.  

Making migrations  

```shell
./manage.py makemigrations  
```

Migrating the tables into database

```shell
./manage.py migrate 
```  

**Create Admin user :**  

```shell
./manage.py createsuperuser  
```  

**Delete whole data from the database :**  

```shell  
./manage.py flush
```  

# Django Basics Part 2 - Simple Crud App  


