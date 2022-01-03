# Django-Live-Project

## Table of Contents

- [About This Project](https://github.com/lytburton/Django-Live-Project#about-this-project)
- [Creating The App](https://github.com/lytburton/Django-Live-Project#creating-the-app-)
- [Creating My Model](https://github.com/lytburton/Django-Live-Project#creating-my-model-)
- [Displaying All Items From the Database](https://github.com/lytburton/Django-Live-Project#displaying-all-items-from-the-database-)
- [Details Page](https://github.com/lytburton/Django-Live-Project#details-page-)
- [Edit and Delete Functions](https://github.com/lytburton/Django-Live-Project#edit-and-delete-functions-)


## About This Project🍂
I participated in a live project over a two week sprint and built an app called "The Gardening App" developed with an MVT structure, and using the Django Framework. My app was part of a larger project called AppBuilder9000. My team used Azure DevOps for project management and version control, and Discord to communicate asynchronously and to hold Scrum meetings. 

During the project, I completed multiple user stories which included creating the Gardening app and registering it within the main AppBuilder9000 project, building a model and model forms, establishing multiple views and URL paths, and creating templates to give the app basic CRUD functionality. The app is also enhanced using Bootstrap 4, Crispy Forms, jQuery, and DataTables.



![This is the home page of the AppBuilder9000 project.](https://github.com/lytburton/Django-Live-Project/blob/main/image1.png?raw=true)


## Creating the App 🍎
In the beginning, I created The Gardening App and registered my app within the main project, AppBuilder9000. I then created my base and home templates using Django block tags, added a function to my views to render the home page, and registered my URLs with the main app. Next, I created URL paths for my homepage, linked The Gardening App's homepage to the AppBuilder9000 home page, and added basic styling and navigation to The Gardening App homepage.



![This is the image link to The Gardening App on the home page of the AppBuilder9000 project.](https://github.com/lytburton/Django-Live-Project/blob/main/image2.png?raw=true)


### Registering My App
```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework',
    'bootstrap4',
    'crispy_forms',
    'Gardening',
]
```

### Base Template
```
{% load static %}

<html lang="en">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <title>{% block title %}My Gardening App{% endblock %}</title>
        <script src="{% static 'js/gardening.js' %}"></script>
    </head>

    <body class="gardening_body">
        <div>
            <!--default navigation and heading for each page-->
            {% block navbar %}
                {% include 'Gardening/navbar.html' %}
            {% endblock %}
            
            <!-- end navigation -->
        </div>
        
         <!-- Page Header -->
        <h2 class="hero_title">{% block heading %} <!--insert each page heading here -->{% endblock %}</h2>


        <!--Page Content-->
        <div>
            {% block content %}
                <!--insert content for each individual page-->
            {% endblock %}
        </div>
        <!-- End Page Content-->


        <!--Footer-->
        {% block footer %}
            {% include 'Gardening/footer.html'%}
        {% endblock %}
        <!-- End Footer-->
        
    </body>
</html>
```

### Home Template
```
<!--This is the home page of the gardening app-->
{% extends "Gardening/gardening_base.html" %}

{% load static %}
<!--Page Header-->
{% block heading %}{% endblock %}

{% block content %}

<!--Cards with page links-->

  <div class="card-deck mx-auto pt-2" style="max-width: 80vw; opacity:90%;">
<!--    Card #1-->
    <a href="#">
      <div class="card text-dark bg-white my-3 ml-3" style="max-width: 18rem; text-align:center;">
        <div class="card-header">Gardening How-To Guides</div>
        <div class="card-body">
          <img class="card-img-top" src="../static/images/gardening3.jpg" alt="Card image cap">
          <h5 class="card-title">Learn gardening with our helpful guides</h5>
        </div>
      </div>
    </a>
<!--    Card #2-->
    <a href="{% url 'create_plant' %}">
      <div class="card text-dark bg-white my-3 ml-3" style="max-width: 18rem; text-align:center;">
        <div class="card-header">My Garden Planner</div>
        <div class="card-body">
          <img class="card-img-top" src="../static/images/gardening1.jpg" alt="Card image cap">
          <h5 class="card-title">Track the dates you sow and harvest</h5>
        </div>
      </div>
    </a>
<!--    Card #3-->
    <a href="#">
      <div class="card text-dark bg-white my-3 ml-3" style="max-width: 18rem; text-align:center;">
        <div class="card-header">Gardening Calendars</div>
        <div class="card-body">
          <img class="card-img-top" src="../static/images/gardening2.jpg" alt="Card image cap">
          <h5 class="card-title">Discover what to plant this season</h5>
        </div>
        </div>
      </div>
    </a>


  </div>
{% endblock %}
```

### Added Function to Views
```
from django.shortcuts import render

# This renders the home page of the gardening app
def gardening_home(request):
    return render(request, "Gardening/gardening_home.html")

```

### Registered URL With the Main App
```
from django.contrib import admin
from django.urls import path, include
from . import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.home, name='home'),
    path('Gardening/', include('Gardening.urls')),
]

```

### URL Path
```
from django.urls import path
from . import views

urlpatterns = [
    path('', views.gardening_home, name='gardening_home'),
]
```

### Image Link From the Main App
```
<!--Gardening link-->
<a href="{% url 'gardening_home' %}" class="grid-item app-image">
   <img src="{% static 'images/flower.jpg' %}" alt="Gardening">
   <div class="fadedbox">
      <div class="title text">Gardening</div>
   </div>
</a>
<!--END of Gardening link-->
```

### Navbar Template
```
{% load static %}
<!--Navbar-->
<nav class="navbar navbar-expand-lg navbar-light sticky-top" style="background-color: #fff;">
<!--  Navbar Title/logo-->
  <a class="navbar-brand font-weight-bold" href="{% url 'gardening_home' %}" style="color: #ff5200;">🍂 THE GARDENING APP</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
<!--  Navigation Items-->
  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav mx-auto">

      <li class="nav-item">
      <!--This links to the home page-->
        <a class="nav-link active pr-5" href="{% url 'gardening_home' %}">HOME<span class="sr-only">(current)</span></a>
      </li>

      <li class="nav-item">
        <!--This links to the garden planner form-->
        <a class="nav-link active px-5" href="{% url 'create_plant' %}">PLAN YOUR GARDEN</a>
      </li>
      <!--        This links to table that shows the users plants stored in the database-->
      <li class="nav-item">
        <a class="nav-link active px-5" href="{% url 'show_plant' %}">MY GARDEN PLANNER</a>
      </li>

    </ul>
  </div>
</nav>
```

### Footer Template
```
{% load static %}

<!--Footer Styling-->
<footer class="page-footer text-center font-small fixed-bottom py-2" style="background-color: #fff;">
        <p class="footer_text">The Gardening App &copy; 2021</p>
</footer>
```


![This is the home page of The Gardening App.](https://github.com/lytburton/Django-Live-Project/blob/main/image3.png?raw=true)


## Creating My Model 🐰
I created a model to collect and track plants that a user might want to grow/are growing in their own garden. A model form was added to give the user the ability to create a new item. When creating my model, I planned out multiple input categories so the user can track the plants in their garden, and included an objects manager for accessing the database. I then added a template to my app for creating a new item,  and a views function that renders the 'create' page (and utilizes the model form to save the collection item to the database). I applied Crispy Forms functionality to enhance the styling, as well.



![This is the model form that receives user input to track data about plants.](https://github.com/lytburton/Django-Live-Project/blob/main/image4.png?raw=true)


### Model
```
from django.db import models

# Choices for plant type selector
TYPE_CHOICES = (
    ('Fruit', 'Fruit'),
    ('Vegetable', 'Vegetable'),
    ('Herb', 'Herb'),
    ('Flower', 'Flower'),
    ('Tree', 'Tree'),
    ('Shrub','Shrub'),
)
# Choices for season planted selector
SEASON_CHOICES = (
    ('Spring', 'Spring'),
    ('Summer', 'Summer'),
    ('Fall', 'Fall'),
    ('Winter', 'Winter'),
)

# Main Garden Planner model
class Plants(models.Model):
    name = models.CharField(max_length=75)
    type = models.CharField(choices=TYPE_CHOICES, max_length=120)
    season_planted = models.CharField(choices=SEASON_CHOICES, max_length=120)
    date_planted = models.DateField()
    days_to_harvest = models.IntegerField()

    def __str__(self):
        return self.name

    objects = models.Manager()

```

### Model Form
```
from django.forms import ModelForm
from .models import Plants
from crispy_forms.helper import FormHelper


# This model form is based on the Plants model class
class PlantsForm(ModelForm):
    helper = FormHelper()
    helper.label_class = 'col-lg-8'


    class Meta:
        model = Plants
        fields = '__all__'
```

### Create Template
```
{% extends 'Gardening/gardening_base.html' %}

{% load static %}

{% load crispy_forms_tags %}
{% crispy form form.helper %}

{% block content %}

<!--This is the container that holds the garden planner form-->
<div class="jumbotron text-white bg-dark py-2" style="width: 60%; margin:0 auto;">
  <h1 style="text-align:center; color:#ff5200;">My Garden Planner</h1>
  <h5 style="text-align:center; color:#ff5200;">Enter information about plants that you have added (or will add!) to your garden.</h5>
  
<!--  This is the garden planner form-->
  <form method="POST" action="" name="create_plant" class="">
    {% csrf_token %}
    
<!--    These are the form field sections-->
    <div class="row d-flex justify-content-center">
      <div class="col-8">
        {{ form.name|as_crispy_field }}
      </div>
    </div>

    <div class="row d-flex justify-content-center">
      <div class="col-4">
        {{ form.type|as_crispy_field }}
      </div>
      <div class="col-4">
        {{ form.season_planted|as_crispy_field }}
      </div>
    </div>

    <div class="row d-flex justify-content-center">
      <div class="col-4">
        {{ form.date_planted|as_crispy_field }}
      </div>
      <div class="col-4">
        {{ form.days_to_harvest|as_crispy_field }}
      </div>
    </div>
    
<!--    This button submits the form-->
    <div class="row d-flex justify-content-center">
      <button type="submit" value="Save" class="btn" style="color:#ff5200;">Submit</button>
    </div>

  </form>
</div>

{% endblock %}
```

### Added Function to Views
```
# This posts the garden planner form to the database
def create_plant(request):
    if request.method == "POST":
        form = PlantsForm(request.POST or None)
        if form.is_valid():
            form.save()
            return redirect("show_plant")
    else:
        form = PlantsForm()
        context = {'form': form}
    return render(request, "Gardening/createPlant_form.html", context)

```

### URL Path
```
from django.urls import path
from . import views

urlpatterns = [
    path('create_plant/', views.create_plant, name="create_plant"),
]
```

## Displaying All Items From the Database 🥕
Here, I displayed information from the database in a new HTML page linked from The Gardening App home page. I added in a function that gets all the items from the database and sends them to the template. I displayed a list of items from the database, with all of the fields for that item displayed with labels/headers. Scrolling, pagination, and a search bar were added using the DataTables plugin.



![This is a searchable and scrollable list of all plants in the database.](https://github.com/lytburton/Django-Live-Project/blob/main/image5.png?raw=true)


### Added Function to Views
```
# This shows what plants are currently in the database
def show_plant(request):
    show_plants = Plants.objects.all()

    context = {'show_plants': show_plants}
    return render(request, "Gardening/show_plant.html", context)
```

### URL Path
```
from django.urls import path
from . import views

urlpatterns = [
    path('show_plant/', views.show_plant, name="show_plant"),
]
```

### Show Template
```
{% extends "Gardening/gardening_base.html" %}

{% load static %}

{% block content %}

<!--This table displays all items in the database-->
<div id="table_container" class="container mx-auto">
    <h2 class="d-inline p-1 my-1 text-success">My Garden Planner🍎🐰🥕☘🍃</h2>
    <hr>
<!--    <div class="spacer"></div>-->
    <table id="plant_table" class="table display table-light table-hover table-striped" style="text-align:center; color:#ff5200;">
<!--        This is the header row of the table-->
        <thead class="thead-light">
        <tr>
          <th scope="col">Plant Name</th>
          <th scope="col">Type</th>
          <th scope="col">Season Planted</th>
          <th scope="col">Date Planted</th>
          <th scope="col">Days to Harvest/Maturity</th>
          <th scope="col">Details</th>
        </tr>
      </thead>
<!--        This is the content added to the table from the database-->
      <tbody>
      {% for plant in show_plants %}
        <tr>
          <th scope="row">{{plant.name}}</th>
          <td>{{plant.type}}</td>
          <td>{{plant.season_planted}}</td>
          <td>{{plant.date_planted}}</td>
          <td>{{plant.days_to_harvest}} days</td>
          <td><a href="{% url 'plant_details' plant.pk %}" name="plant_details">See details for this plant</a></td>
        </tr>
      {% endfor %}
      </tbody>
    </table>
</div>

{% endblock %}
```

## Details Page ☘
Next, I created a 'details' template page that shows the details of any single item from within the database, as selected by the user. After registering the URL pattern, I created a views function that will find a single item from the database and send it to the template. I added in a link for each item on the 'display all items' page that will direct to the 'details' page for that item, and displayed all the details of the item.



![This page shows the details of a single plant a user selects from the database.](https://github.com/lytburton/Django-Live-Project/blob/main/image6.png?raw=true)


### Details Template
```
{% extends "Gardening/gardening_base.html" %}

{% load static %}

{% block content %}
<!--This table displays all items in the database-->
<div id="table_container" class="container mx-auto">
    <h2 class="d-inline p-1 my-1 text-success">{{ details.name }} Details</h2>
    <hr>
<!--    <div class="spacer"></div>-->
    <table class="table display table-light table-hover table-striped" style="text-align:center; color:#ff5200;">
<!--        This is the header row of the table-->
        <thead class="thead-light">
        <tr>
          <th scope="col">Plant Name</th>
          <th scope="col">Type</th>
          <th scope="col">Season Planted</th>
          <th scope="col">Date Planted</th>
          <th scope="col">Days to Harvest/Maturity</th>
        </tr>
      </thead>
<!--        This is the content added to the table from the database-->
      <tbody>
        <tr>
          <th scope="row">{{details.name}}</th>
          <td>{{details.type}}</td>
          <td>{{details.season_planted}}</td>
          <td>{{details.date_planted}}</td>
          <td>{{details.days_to_harvest}} days</td>
        </tr>
      </tbody>
    </table>
    <a href="{% url 'edit_plant' details.pk %}" name="edit_plant">
        <button type="submit" name="edit_plant" class="btn btn-success">Edit</button>
    </a>
        <button type="button" class="btn btn-danger" data-toggle="modal" data-target="#myModal">Delete</button>


</div>

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLongTitle">Are you sure you want to delete this plant?</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        The plant you selected will be permanently deleted from My Garden Planner!
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">No, go back!</button>
        <a href="{% url 'delete_plant' details.pk %}">
            <button type="button" class="btn btn-danger">Yes, delete it!</button>
        </a>

      </div>
    </div>
  </div>
</div>

{% endblock %}
```

### URL Path
```
from django.urls import path
from . import views

urlpatterns = [
    path('<int:pk>/plant_details/', views.plant_details, name="plant_details"),
]
```

### Added Function to Views
```
# This generates a page of details for each plant in the database
def plant_details(request, pk):
    details = get_object_or_404(Plants, pk=pk)

    context = {'details': details}
    return render(request, "Gardening/gardening_details.html", context)
```

## Edit and Delete Functions 🍃
These additions allow for edit and delete functions to be done from the details page. There is also a confirmation that is presented before deleting. I added an edit page to the templates, a URL pattern for this template, and I used model forms and instances to display the content of a single item from the database. I had the views function send the information for the single item and save any changes. Within the details template, I included the option to delete an item with a modal confirmation pop-up to ensure that the user wants to delete.



![This is the page that allows a user to edit plant information.](https://github.com/lytburton/Django-Live-Project/blob/main/image7.png?raw=true)



![This is the confirmation a user receives before deleting a plant from the database.](https://github.com/lytburton/Django-Live-Project/blob/main/image8.png?raw=true)


### Edit Template
```
{% extends 'Gardening/gardening_base.html' %}

{% load static %}

{% load crispy_forms_tags %}
{% crispy form form.helper %}

{% block content %}

<!--This is the container that holds the garden planner edit form-->
<div class="jumbotron text-white bg-dark py-2" style="width: 60%; margin:0 auto;">
  <h1 style="text-align:center; color:#ff5200;">Edit Plant Details</h1>
  
<!--  This is the form that allows a user to edit a plant in the database-->
  <form method="POST" name="edit_plant">
    {% csrf_token %}
    
<!--    These are the form field sections-->
    <div class="row d-flex justify-content-center">
      <div class="col-8">
        {{ form.name|as_crispy_field }}
      </div>
    </div>

    <div class="row d-flex justify-content-center">
      <div class="col-4">
        {{ form.type|as_crispy_field }}
      </div>
      <div class="col-4">
        {{ form.season_planted|as_crispy_field }}
      </div>
    </div>

    <div class="row d-flex justify-content-center">
      <div class="col-4">
        {{ form.date_planted|as_crispy_field }}
      </div>
      <div class="col-4">
        {{ form.days_to_harvest|as_crispy_field }}
      </div>
    </div>
<!--    This button submits the form-->
    <div class="row d-flex justify-content-center">
      <button type="submit" value="Save" class="btn" style="color:#ff5200;">Update</button>

    </div>

  </form>
</div>

{% endblock %}
```

### URL Paths
```
from django.urls import path
from . import views

urlpatterns = [
    path('<int:pk>/edit_plant/', views.edit_plant, name='edit_plant'),
    path('<int:pk>/delete_plant/', views.delete_plant, name='delete_plant'),
]
```

### Added Functions to Views
```
# This allows the user to edit a specific plant in the garden planner
def edit_plant(request, pk):
    show_plants = Plants.objects.get(pk=pk)
    form = PlantsForm(request.POST, request.FILES, instance=show_plants)
    if request.method == "POST":
        if form.is_valid():
            form2 = form.save(commit=False)
            form2.user = request.user
            form2.save()
            return redirect("show_plant")
    else:
        form = PlantsForm(instance=show_plants)
        context = {'form': form, 'show_plants': show_plants}
    return render(request, "Gardening/edit_plant.html", context)


# This allows the user to delete a specific plant from the garden planner
def delete_plant(request, pk):
    show_plants = Plants.objects.get(pk=pk)
    show_plants.delete()
    return redirect("show_plant")

```

### Modal With Delete Confirmation
```
<div class="modal-body">
        The plant you selected will be permanently deleted from My Garden Planner!
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">No, go back!</button>
        <a href="{% url 'delete_plant' details.pk %}">
            <button type="button" class="btn btn-danger">Yes, delete it!</button>
        </a
      </div>
</div>
```
