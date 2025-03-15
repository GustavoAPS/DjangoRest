# DjangoRest

This repository is for studying and practicing Django REST Framework (DRF) concepts.

## Table of Contents

* Project Setup (Virtual Environment)
* Common DRF Concepts
* Useful Commands (Django)
* Troubleshooting

## Project Setup (Virtual Environment)

1.  **Create a virtual environment:**

    ```bash
    python -m venv venv
    ```

2.  **Activate the virtual environment:**

    ```bash
        source venv/bin/activate
    ```

4.  **Install dependencies:**

    If there is a requirements.txt file:
    
    ```bash
        pip install -r requirements.txt
    ```
    Else:
    
    ```bash
        pip install django
        pip install djangorestframework
        pip freeze > requirements.txt
    ```

6.  **Run migrations:**

    If there are migration files:

    ```bash
    python manage.py migrate
    ```

    Else:

    ```bash
        python manage.py makemigrations
        python manage.py migrate
    ```

8.  **Create a superuser (optional):**

    ```bash
    python manage.py createsuperuser
    ```

9.  **Run the development server:**

    ```bash
        python manage.py runserver
    ```

## Common DRF Concepts

* **Serializers:**
    * Convert complex data (like Django model instances) to Python data types that can be easily rendered into JSON, XML, or other content types.
    * Also handle deserialization (converting incoming data back into model instances).
* **ViewSets:**
    * Provide a way to group related views into a single class, reducing code duplication.
    * Offer common actions like `list`, `create`, `retrieve`, `update`, and `destroy`.
* **Routers:**
    * Automatically generate URL patterns for ViewSets, simplifying URL configuration.
* **Permissions:**
    * Control access to API endpoints based on user authentication and authorization.
    * Common permissions include `IsAuthenticated`, `IsAdminUser`, and custom permissions.
* **Authentication:**
    * Verify the identity of API clients.
    * DRF supports various authentication schemes, including basic authentication, token authentication, and OAuth.
* **Generic Views:**
    * Pre-built views that provide common API functionality, reducing the amount of code you need to write.
* **Filters:**
    * Allow to filter the results of a list view.
* **Pagination:**
    * Divide large result sets into smaller, manageable pages.


## Useful Commands (Django)

| Command | Description |
|---------|-------------|
| `django-admin startproject project_name`                | Creates a new Django project |
| `python manage.py startapp app_name`                    | Creates a new Django app |
| `python manage.py runserver`                            | Starts the development server (default: 127.0.0.1:8000) |
| `python manage.py makemigrations`                       | Creates migration files based on model changes |
| `python manage.py migrate`                              | Applies migrations to the database |
| `python manage.py createsuperuser`                      | Creates an admin superuser account |
| `python manage.py shell`                                | Opens an interactive Python shell with Django settings loaded |
| `python manage.py collectstatic`                        | Collects static files for deployment |
| `python manage.py test`                                 | Runs Django unit tests |
| `python manage.py check`                                | Checks for common issues in the project |
| `python manage.py showmigrations`                       | Lists all migrations and their status |
| `python manage.py sqlmigrate app_name migration_number` | Shows the SQL commands for a migration |
| `python manage.py flush`                                | Deletes all data from the database (keeps migrations) |
| `python manage.py dumpdata app_name.Model --format=json`| Exports data from a model to JSON |
| `python manage.py loaddata data.json`                   | Loads data from a JSON file into the database |
| `python manage.py changepassword username`              | Changes a user's password |
| `django-admin help`                                     | Displays help for available commands |

## Naming Conventions

| **Component**                 | **Naming Convention**                                                      | **Example**                          |
|-------------------------------|-----------------------------------------------------------------------------|--------------------------------------|
| **Project Name**               | Lowercase with underscores                                                  | `my_project`                         |
| **App Names**                  | Lowercase with underscores                                                  | `blog`, `user_profiles`, `shop`      |
| **Model Names**                | Singular, Capitalized, CamelCase                                            | `Post`, `Category`, `UserProfile`    |
| **Field Names**                | Lowercase with underscores                                                  | `title`, `date_created`, `user_profile` |
| **Foreign Keys / Related Names** | Lowercase model name for ForeignKey, use `related_name` for reverse lookup | `author`, `category`, `posts`        |
| **View Names (FBV)**           | Lowercase with underscores                                                  | `home_view`, `post_detail`           |
| **View Names (CBV)**           | Capitalized, CamelCase                                                     | `PostDetailView`, `UserProfileCreateView` |
| **Template Names**             | Lowercase with underscores, app-specific directories                        | `blog/post_list.html`, `user_profiles/user_form.html` |
| **URL Pattern Names**          | Lowercase with underscores                                                  | `home`, `post_detail`                |
| **Static Files**               | Organize by type (css, js, images)                                          | `static/css/style.css`, `static/js/main.js` |
| **Media Files**                | Organize with `MEDIA_ROOT` setting for uploads                               | `media/uploads/profile_picture.jpg`  |
| **Manager and Queryset Methods** | Lowercase form of model name, followed by `_manager`                       | `Post.objects.all_posts()`           |
| **Custom Template Tags/Filters** | Lowercase with underscores, inside `templatetags` directory                | `my_app/templatetags/custom_tags.py`, `my_app/templatetags/custom_filters.py` |
| **Form and Serializer Names**  | Singular, Capitalized                                                       | `PostForm`, `UserProfileSerializer`  |
| **Test Names**                 | Use `test_` prefix for test methods and test files                          | `test_views.py`, `test_models.py`, `test_user_registration` |
| **Constants**                  | Uppercase with underscores                                                  | `MAX_USERS`, `DEFAULT_PAGE_SIZE`     |


## Troubleshooting

* **Dependency errors:**
    * Ensure that all dependencies are listed in `requirements.txt`.
    * Make sure your virtual environment is activated.
    * Try deleting your virtual environment and recreating it.
* **Database connection errors:**
    * Verify the database credentials in Django settings.
    * Make sure your database server is running.
* **API errors:**
    * Check the terminal output for error messages.
    * Use the Django debug toolbar (if enabled) to inspect requests and responses.
* **Migrations issues:**
    * Make sure you run `makemigrations` and `migrate` after making changes to your models.
    * If you have a migration conflict, you may need to resolve it manually.
* **Port conflicts:**
    * If port 8000 is already in use, specify a different port when running the development server: `python manage.py runserver 8080`.



Links:

Authentication:<br>
- https://www.turing.com/kb/django-rest-framework-authentication

Viewsets:<br>
- https://www.django-rest-framework.org/api-guide/viewsets/#:~:text=Django%20REST%20framework%20allows%20you,single%20class%2C%20called%20a%20ViewSet%20.

- https://medium.com/@ukemeboswilson/understanding-and-implementing-views-in-django-rest-framework-2184eceb7336