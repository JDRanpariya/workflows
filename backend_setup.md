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
