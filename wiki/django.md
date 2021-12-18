# Django

## Quickstart commands 
* Start a project: 
`django-admin startproject {project_name}`

* Run server:
`python manage.py runserver` 

* Create a new app:
1. `python manage.py startapp {app_name}` 
2. Add the app name to the `INSTALLED_APPS` in settings.py

* Start the Django shell
python manage.py shell

## View 
* A view contains logic for how to populate a template given a particular request object
```
from django.http import JsonResponse
from django.shortcuts import render
from dashboard.models import Order
from django.core import serializers

def dashboard_with_pivot(request):
    return render(request, 'dashboard_with_pivot.html', {})
```

* To map a view function to a url, we use {project_name}/urls.py and {app_name}/urls.py
 
```project/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('dashboard/', include('dashboard.urls')),
]
```

```app/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.dashboard_with_pivot, name='dashboard_with_pivot'),
    path('data', views.pivot_data, name='pivot_data'),
]
```

## Template 
* Templates are HTML to be filled by view logic
```
<head>
  <meta charset="UTF-8">
  <title>Dashboard with Flexmonster</title>
  <script src="https://cdn.flexmonster.com/flexmonster.js"></script>
  <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
  <link rel="stylesheet" href="https://cdn.flexmonster.com/demo.css">
</head>
<body>
<div id="pivot-table-container" data-url="{% url 'pivot_data' %}"></div>
<div id="pivot-chart-container"></div>
</body>
```

## Model 
* Conceptual representation of data stored in our db
* Migration is a file that describes which changes to be applied to the database. 
* When we need to create a database based on the model described in a Python model class, use migration:
`python manage.py makemigrations dashboard`

```
from django.db import models

class Order(models.Model):
    product_category = models.CharField(max_length=20)
    payment_method = models.CharField(max_length=50)
    shipping_cost = models.CharField(max_length=50)
    unit_price = models.DecimalField(max_digits=5, decimal_places=2)
```

## Forms 
* Forms provide a way to accept input from the user and do some backend processing on a datatype that represents that input
```
from django import forms

class ChartInputsForm(forms.Form):
    ticker = forms.CharField(label="Ticker", max_length=100)
    expiry = forms.CharField(label="Expiry", max_length=100)
```

* An empty form can be provided to render some default HTML for accepting the form input.
In views.py:
```
def gen_empty_form_prompt(request) -> HttpResponse:
    context = {"form": ChartInputsForm()}
    return render(request, "vol_curve_charts.html", context)
```

* Then in the template HTML it can be used like so:
```
<form action="my_action/" method="post">
    {% csrf_token %}
    {{ form }}
    <input type="submit" value="Submit">
</form>
```

* When the user actually submits the form, the backend will call whatever function is mapped to the "my_action/" url in urls.py, and the form inputs will be captured in the request.
In views.py:
```
def gen_form_response(request) -> HttpResponse:
    inputs = ChartInputsForm(request.POST)
    ticker = inputs['ticker'].value()
    ...
    return render(request, "vol_curve_charts.html", context)
```
