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

Page 30 mentions `git init` so we can start a fresh repository and commit our changes

Up until page 38 they talk about Git and Bitbucket so I skip this section as I know enough about this to get by.

Page 39 and 40 explain initial set up to get a project up and running

Next few pages discuss where to put the templates folder so Django can look for it. The way we do here is creating a template folder in the BASE_DIR level where manage.py is and edit `settings.py` to add the code below:

Page 43,

```
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```