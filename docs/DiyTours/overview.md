# DIYTours App Documentation

Welcome to the DIYTours app! This reusable Django app is designed for developers who want to manage and showcase tours seamlessly. With essential features like categories, locations, pricing, and a gallery for images, DIYTours helps you create a robust tour management system. Let’s dive into how to install, integrate, and customize the app!

## Table of Contents

	1.	Features
	2.	Requirements
	3.	Installation
	4.	Setup in Django
	5.	Using DIYTours
	6.	Customizing the App
	7.	Deployment
	8.	Contribution

## Features

	•	Tours Management: Create and manage various tours with details like title, description, and pricing.
	•	Image Gallery: Upload and showcase images for each tour.
	•	Categories and Locations: Organize tours by categories and locations for easy navigation.
	•	Promotions: Add promotional prices for tours based on specific dates.
	•	Comments: Allow users to leave comments on tours for engagement.

## Requirements

Before you start, ensure you have the following installed on your machine:

	•	Python 3.7 or higher
	•	Django 5.0 or higher
	•	Pillow (for handling images)
	•	Git

## Installation

To get started with DIYTours, you need to set up a Django project. Navigate to your desired directory and execute the following command to create a new project:

```shell
django-admin startproject ProjectName
```

This command creates a new directory with your project name. Next, clone the DIYTours repository by running:

```shell
git clone https://github.com/DjangoDIY/diytours.git
```

This downloads the DIYTours app into your current directory. Now, navigate into the DIYTours directory:

```shell
cd diytours
``` 

Move the App to Your Project

Inside the diytour directory, you’ll find the app’s source code in a subdirectory named diytours. Move this directory into your Django project:

```shell
mv diytours /path/to_your_project/ProjectName
```

Update Your Django Project

Now, go to your project directory and open the settings.py file. Add 'tours' to the INSTALLED_APPS list:

```py title="ProjectName/settings.py" hl_lines='2'
INSTALLED_APPS = [
    'diytours',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

Next, set up media files for the app. In the same settings.py, add the following configuration:

```py  title="ProjectName/settings.py"
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```
## Configure URLs

Open your project’s urls.py file and include the URLs for the DIYTours app:

```py title="ProjectName/urls.py" hl_lines="8-12"
from django.contrib import admin
from django.urls import path, include
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('tours/', include('tours.urls')),
]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```
## Run Migrations

Now that your app is integrated, apply the migrations to create the necessary database tables:

```shell
python manage.py migrate
```
## Create a Superuser

Next, create a superuser to access the Django admin interface:
```shell
python manage.py createsuperuser
```
Follow the prompts to set up your superuser account. Once you log in to the admin panel, you’ll see the DIYTours app ready for use.

Start the Development Server

Now, let’s fire up the Django development server:
```shell
python manage.py runserver
```
And that’s it! Your DIYTours app is now installed and fully functional. Happy touring!

## Using DIYTours

Adding new tours is easy! Simply navigate to the Django admin panel at /admin, and under the Tours section, you can add new Categories, Tours, Dates, Promotions, and Images.

	•	Adding a New Tour: Upload a featured image for the tour and attach multiple images for the gallery.

## Customizing the App

If you want to make modifications to the app, here’s how you can do it:

Customizing the Models

Open the models.py file in the tours app to modify existing models or add new fields. For example, if you want to add a custom field to the Tour model:

```py title="diytours/models.py"
class Tour(models.Model):
    ...
    custom_field = models.CharField(max_length=255, blank=True, null=True)
```
## Run the migrations to apply your changes:

```shell
python manage.py makemigrations tours
python manage.py migrate
```
## Template Customization

The app uses templates to render tour details. To customize the look and feel, you can override the default templates. Create a directory templates/tours/ in your project and add a details.html file.

Example content for details.html:
```html title="index.html"
{% extends 'base.html' %}
{% block content %}
    <h1>{{ tour.title }}</h1>
    <div class="gallery">
        <img src="{{ tour.featured_image.url }}" alt="{{ tour.title }} image">
        {% for image in tour.images.all %}
            <img src="{{ image.image.url }}" alt="Additional image">
        {% endfor %}
    </div>
    <p>{{ tour.description }}</p>
{% endblock %}
```
## Deployment

When you’re ready to deploy your app, consider the following:

1.	Static and Media Files: Configure your web server (like Nginx) to serve static and media files.
2.	Security: Set DEBUG = False and update ALLOWED_HOSTS in your settings.py.
3.	Database: Use a production database like PostgreSQL and update the DATABASES setting.
4.	Collect Static Files: Run the command to collect all static files for production use:

python manage.py collectstatic

## Contribution

We welcome contributions to the DIYTours app! Here’s how you can contribute:

1. Fork the repository.
2.	Create a new branch for your feature:
```shell
git checkout -b feature-branch
```

3.	Make your changes and commit:
```shell
            git commit -m "Added a new feature"
```

4.	Push to your branch:
```shell
            git push origin feature-branch
```

5.	Submit a pull request for review.

