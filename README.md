# DjangoRest

This repository is for studying and practicing Django REST Framework (DRF) concepts.

## Table of Contents

* Project Setup (Virtual Environment)
* Common DRF Concepts
* Useful Commands (Django)
* Troubleshooting

## Project Setup (Virtual Environment)

1.  **Clone the repository:**

    ```bash
    git clone <repository_url>
    cd <repository_name>
    ```

2.  **Navigate to the backend directory:**

    ```bash
    cd backend
    ```

3.  **Create a virtual environment:**

    ```bash
    python -m venv venv
    ```

4.  **Activate the virtual environment:**

    * **On macOS and Linux:**

        ```bash
        source venv/bin/activate
        ```

    * **On Windows:**

        ```bash
        venv\Scripts\activate
        ```

5.  **Install dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

6.  **Run migrations:**

    ```bash
    python manage.py migrate
    ```

7.  **Create a superuser (optional):**

    ```bash
    python manage.py createsuperuser
    ```

8.  **Run the development server:**

    ```bash
    python manage.py runserver
    ```

9.  **Access the API:**

    * The API will be available at `http://127.0.0.1:8000/`.

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

* **Run migrations:**

    ```bash
    python manage.py migrate
    ```

* **Create a superuser:**

    ```bash
    python manage.py createsuperuser
    ```

* **Run the development server:**

    ```bash
    python manage.py runserver
    ```

* **Create a new Django app:**

    ```bash
    python manage.py startapp <app_name>
    ```

* **Run tests:**

    ```bash
    python manage.py test
    ```

* **Make migrations:**

    ```bash
    python manage.py makemigrations
    ```

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
