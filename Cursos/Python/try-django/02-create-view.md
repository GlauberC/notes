## Conteúdos

- create a view
- import homepage

# create a view

## src/try_django/views.py

```py
from django.http import HttpResponse



def contact_page(request):
    return HttpResponse("<h1>Contact us</h1>")


def about_page(request):
    return HttpResponse("<h1>About us</h1>")

```

# import homepage

## src/try_django/urls.py

```py
from django.contrib import admin
from django.urls import path

from .views import (contact_page, about_page)

urlpatterns = [
    path('admin/', admin.site.urls),
    path('about/', about_page),
    path('contact/', contact_page)
]

```
