# DIYBlog App Documentation

Welcome to the DIYBlog app! DIYBlog is a reusable Django app that provides essential blogging functionality such as posts, categories, tags, and comments. This app is designed for developers with basic knowledge of Python and Django. Follow the instructions below to install and integrate DIYBlog into your Django project.

## Sections

	1.	Features
	2.	Requirements
    3.	Installation
    4.	Setup in Django
    5.	Usage
	6.	License

### Features

	•	Posts: Create and manage blog posts.
	•	Categories: Organize posts by category.
	•	Tags: Tag posts for easy filtering.
	•	Comments: Allow readers to leave comments on posts.

### Requirements

	•	Python 3.10 or higher
	•	Django 4.x or higher


### Installation

To start using DIYBlog, you’ll first need to set up a Django project. Navigate to your desired directory and execute the following command to start a new project:

```py title="startting project" linenums="1"
django-admin startproject ProjectName
```
This command creates a new directory with your project name. Now, to integrate the DIYBlog app into your project, clone the repository by running:


```shell 
git clone https://github.com/DjangoDIY/diyblog.git
```
This will download the DIYBlog app into your current directory. The next step is to move the app into your Django project. Navigate to the diyblog directory:

```shell
cd diyblog
```
Inside this directory, you’ll find the app’s source code in a subdirectory named diyblog. Move this directory into your Django project:

```shell
mv diyblog /path/to_your_project/ProjectName
```

Once the app is moved, head over to your project directory and open the settings.py file. Under the INSTALLED_APPS section, add 'diyblog' as shown below:

```s hl_lines='2'

INSTALLED_APPS = [
    'diyblog',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

Now, we need to set up the URLs for DIYBlog. Open your project’s urls.py file and include the DIYBlog app’s URLs:


```py title="ProjectName/urls.py" hl_lines='6'

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path("blog/",include("diyblog.urls"))

]
```

At this point, the DIYBlog app is integrated into your project. To complete the setup, you need to run migrations to create the necessary database tables.

### Migrations

Run the following command to apply migrations:

```py
python manage.py migrate

```

If the migrations run successfully, you should see output similar to the following:

```
  Applying auth.0012_alter_user_first_name_max_length... OK
  Applying blog.0001_initial... OK
  Applying blog.0002_post_category... OK
  Applying sessions.0001_initial... OK
```

### Superuser Setup


Next, create a superuser to access the Django admin interface:

```py 
python manage.py createsuperuser

```
Follow the on-screen prompts to create the superuser. After logging in to the admin panel, you should see the DIYBlog app ready for use.


Now let's fire up our Django Runserver

```py 
python manage.py runserver
```


And that’s it! Your DIYBlog app is now installed and fully functional.

Happy Blogging!



