# Book notes

Up until page 24 we get an overview of Django and how to install and run a local server.

Page 25 we create an app running

`python manage.py startapp pages`

Page 27 adds a new item to INSTALLED_APPS in settings.py

`'pages.apps.PagesConfig'`

Page 28 creates the views.py code

```
from django.http import HttpResponse

def homePageView(HttpResponse):
    return HttpResponse('Hello, World!')
```

In page 29 we create a new urls.py under the pages folder (there are 2 now, one for the project and one for the page)

- urls.py under pages

```
from django.urls import path

from .views import homePageView

urlpatterns = [
    path('', homePageView, name='Home')
]
```