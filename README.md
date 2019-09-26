# django-REST

## Project Agenda

1. API Endpoints
	- CRUD (url)
		- Retrieve Update and Delete
		

2. HTTP Methods
	- GET, POST, PATCH, DELETE

3. Data Types and Validation
	- JSON -> Serializer
	- Validation -> Serializer
	
## Installations:

### pip
	- sudo apt install pip

### django
	- pip install Django==2.0

### Django RestFramework
	- pip install Djangorestframework



## Create project for REST API

	- django-admin startproject `api_example`

### Migrations
	
	-	python manage.py makemigrations

	-	python manage.py migrate

### Create admin Super user

	- python manage.py createsuperuser

### Create App for REST API

	Change directory to project and inside the project need to create APP

	- django-admin startapp `language`



### Add to Settings for rest_framework

	- Open settings.py file and inside that file we need to add `rest_framework` and `language` to INSTALLED APP's

### Add app(language) route to urls
	
	- open api_example/urls.py

	`from django.contrib import admin
	 from django.urls import path,include

	 urlpatterns = [
    	 path('admin/', admin.site.urls),
    	 path('',include('languages.urls'))
	 ]`	

### Serialize for API
	
	- We need to create `serializers.py` inside languages App

		`from rest_framework import serializers
		 from .models import Language

         class LanguageSerializer(serializers.HyperlinkedModelSerializer):
			class Meta:
				model=Language
				fields=('id','url','name','paradign')
		`

### languages/models.py

	`from django.db import models

	 class Language(models.Model):

	 name=models.CharField(max_length=100)
	 paradign=models.CharField(max_length=100)

		 def __str__(self):
		 	return self.name`

	* Migrations
		-	python manage.py makemigrations

		-	python manage.py migrate
 
### languages/views.py

	`from django.shortcuts import render
	 from rest_framework import viewsets
	 from .models import Language
	 from .serializers import LanguageSerializer


	 class LanguageView(viewsets.ModelViewSet):
		 queryset=Language.objects.all()
	 	 serializer_class=LanguageSerializer`

### languages/urls.py file

	`from django.urls import path,include
	 from . import views
	 from rest_framework import routers

	 router=routers.DefaultRouter()
     router.register('languages',views.LanguageView)

	 urlpatterns=[
	 path('',include(router.urls))

	]
	`

### Now add to admin sites to models

	- Open admin.py and add admin sites

	`from django.contrib import admin
	 from .models import Language


	 admin.site.register(Language)`


