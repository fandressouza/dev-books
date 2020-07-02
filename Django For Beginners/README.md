# Book notes

## Initial set up (From page 0 to 49)

Skipped pages 1-24 - I had Django installed at this point so not wasting much time

Up until page 24 we get an overview of Django and how to install and run a local server.

Page 25 we create an app running

`python manage.py startapp pages`

Page 27 adds a new item to INSTALLED_APPS in `settings.py`

```python
INSTALLED_APPS = [
    'pages.apps.PagesConfig', #added this item
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

Page 28 creates the `views.py` code

```python
from django.http import HttpResponse

def homePageView(HttpResponse):
    return HttpResponse('Hello, World!')
```

In page 29 we create a new `urls.py` under the pages folder (there are 2 now, one for the project and one for the page)

`urls.py` under pages:

```python
from django.urls import path

from .views import homePageView

urlpatterns = [
    path('', homePageView, name='Home')
]
```
Run the app by using the command below:

`python manage.py runserver`

---

Page 30 mentions `git init` so we can start a fresh repository and commit our changes

Up until page 38 they talk about Git and Bitbucket so I skip this section as I know enough about this to get by.

---

Page 39 and 40 explain initial set up to get a project up and running

Next few pages discuss where to put the templates folder so Django can look for it. The way we do here is creating a template folder in the BASE_DIR level where manage.py is and edit `settings.py` to add the code below:

Page 43,

```python
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

In page 45 we modify `pages/views.py` to point to the newly created template from previous pages.


`pages/views.py`
```python
from django.views.generic import TemplateView

class HomePageView(TemplateView):
    template_name = 'home.html'

class AboutPageView(TemplateView):
    template_name = 'about.html'
```

`pages/urls.py`
```python
from django.urls import path

from .views import HomePageView, AboutPageView

urlpatterns = [
    path('about/', AboutPageView.as_view(), name='about'),
    path('', HomePageView.as_view(), name='home')
]
```

Also, edit the project-level `urls.py` to add the path for the new templates:

`pages/urls.py`
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('pages.urls')), #new
]
```

Last, you need to go to the templates folder and create the template for `about.html`

---

## Extending Templates (page 49)

At this point we explore extending templates and adding a **base** template which will be used for all pages.

We create base.html and add the code below to both home.html and about.html

base.html
```html
<header>
    <a href="{% url 'home' %}">Home</a> | <a href="{% url 'about' %}">About</a>
</header>

{% block content %}

{% endblock content %}
```

about.html
```html
{% extends 'base.html' %}


{% block content %}

<h1>About Page</h1>

{% endblock content %}
```

home.html
```html
{% extends 'base.html' %}


{% block content %}

<h1>Home Page</h1>

{% endblock content %}
```

## Page 53 touches on tests

In this example the book is using **SimpleTestCase** which is a basic version of **TestCase**

Test pages status using the code below

```python
from django.test import SimpleTestCase

class SimpleTests(SimpleTestCase):
    def test_home_page_status_code(self):
        response = self.client.get('/')
        self.assertEqual(response.status_code, 200)

    def test_about_page_status_code(self):
        response = self.client.get('/about/')
        self.assertEqual(response.status_code, 200)
```

To run the test go to the root of the project (where manage.py is)

`python manage.py test`

Page 54 to 56 touches on Git