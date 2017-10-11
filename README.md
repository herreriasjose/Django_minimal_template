Django without the fluff
========================
When you type...
```
$ django-admin.py startproject my_project
```
...you are basically setting up a lot of configuration files together. But a minimal Django application could be something like this:

```python
# minimal.py

""" A minimal Django template. """
import sys
from django.conf import settings 
# Notice we are not doing all the imports here

settings.configure(DEBUG=True,SECRET_KEY='secret',ALLOWED_HOSTS=['127.0.0.1','localhost'],
ROOT_URLCONF=__name__, MIDDLEWARE_CLASSES=('django.middleware.common.CommonMiddleware',),)

# This 'special' import sequence is necessary. Since Django expects certain
# settings performed before the rest of imports. 

from django.conf.urls import url
from django.http import HttpResponse

# The "view"

def index(request):
    return HttpResponse("Hello, World!")
    
urlpatterns = (
    url(r'^$',index),
    url(r'^index$',index),
    )

if __name__ == "__main__":

    from django.core.management import execute_from_command_line
    execute_from_command_line(sys.argv)
```

This script works as a functional (not ready for production) Django project. You could run the development server this way:
```
$ python minimal.py runserver 80
```
And get this:


![Django Minimal](https://raw.githubusercontent.com/herreriasjose/Django_minimal_template/master/django_minimal.png)
