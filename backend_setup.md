# Django

### general setup
```
pipenv install django python-dotenv --skip-lock

pipenv shell

django-admin startproject projectname .  // . for current dir

cd projectname
```
- add follwing to setting.py
```
import os
from dotenv import load_dotenv, find_dotenv
load_dotenv(find_dotenv())

// now replace your secrets with env variable
SECRET_KEY = os.getenv('SECRET_KEY')
```
- create .env & .env.example with following content
``` 
SECRET_KEY = "you secret django token" 
```

## django-graphene setup
- `pipenv install django-cors-headers django-graphql-jwt graphene-django psycopg2 --skip-lock` 
- add follwing to setting.py
```
'graphene_django', # in installed apps

GRAPHENE = {
    'SCHEMA': 'nsfw_api.schema.schema',
    'MIDDLEWARE': [
        'graphql_jwt.middleware.JSONWebTokenMiddleware',
    ],
}  

AUTHENTICATION_BACKENDS = [
    'graphql_jwt.backends.JSONWebTokenBackend',
    'django.contrib.auth.backends.ModelBackend',
]

MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',

]

CORS_ALLOWED_ORIGINS = [
    "http://localhost:3000",
    "http://localhost:5433"
]
```
- add following to urls.py
```
from django.contrib import admin
from django.urls import path
from graphene_django.views import GraphQLView
from django.views.decorators.csrf import csrf_exempt

urlpatterns = [
    path('admin/', admin.site.urls),
    path('graphql/', csrf_exempt(GraphQLView.as_view(graphiql=True)))

]
```

