# Models 

Models are the database layout of Django with additional metadata.

# Introduction

- [Simple Model](#simple-model)
- [Model Fields](#model-fields)
- [Model-Level Validation](#model-level-validation)
- [Getting Help](#getting-help)

## Simple model

The most simple way to create a model in Django is to create a class that subclasses `django.db.models.Model`.

```python
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField("date published")


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

## Model Fields

### 🔍 List of Common Django Model Fields

| Field Type | Description |
|------------|-------------|
| `models.CharField(max_length=255)` | A short text field (`max_length` is required) |
| `models.TextField()` | A large text field (no `max_length` required) |
| `models.IntegerField()` | Stores an integer |
| `models.FloatField()` | Stores a floating-point number |
| `models.BooleanField(default=False)` | A True/False field |
| `models.DateField(auto_now_add=True)` | Stores a date |
| `models.DateTimeField(auto_now_add=True, auto_now=True)` | Stores date & time |
| `models.ForeignKey(Model, on_delete=models.CASCADE)` | Creates a one-to-many relationship |
| `models.ManyToManyField(Model)` | Creates a many-to-many relationship |
| `models.EmailField()` | Stores an email address |
| `models.ImageField(upload_to="images/")` | Stores an image file |

---

### 🛠 How to See Required & Optional Arguments?

Each field type has its own required and optional arguments.

For example, **CharField**:
```python
name = models.CharField(
    max_length=100,  # ✅ Required: Max length
    unique=True,     # Optional: Makes it unique
    blank=True,      # Optional: Allows empty values
    null=True        # Optional: Stores NULL in DB
)
```

### 📌 Main Arguments (Common to Most Fields)

| Argument | Description |
|----------|-------------|
| `max_length` | Required for `CharField`, sets max length |
| `default=value` | Sets a default value |
| `null=True` | Allows NULL values in DB |
| `blank=True` | Allows empty values in forms |
| `unique=True` | Ensures unique values |
| `choices=[('A', 'Option A'), ('B', 'Option B')]` | Dropdown-style choices |

---

## Model-Level Validation

Django provides multiple ways to enforce **validation at the model level** to ensure data consistency.

### 🔹 Using `clean()` Method for Custom Validation

The `clean()` method allows you to define validation logic before saving the model.

```python
from django.core.exceptions import ValidationError
from django.db import models


class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)

    def clean(self):
        if self.price <= 0:
            raise ValidationError("Price must be greater than zero.")
```

To trigger `clean()` when saving an object, use:

```python
from django.core.exceptions import ValidationError

product = Product(name="Laptop", price=-50.00)

try:
    product.full_clean()  # This will raise ValidationError
    product.save()
except ValidationError as e:
    print(e)
```

---

### 🔹 Overriding `save()` for Pre-Save Validation

You can override the `save()` method to enforce validation before saving data.

```python
class Order(models.Model):
    order_number = models.CharField(max_length=20, unique=True)
    total_price = models.DecimalField(max_digits=10, decimal_places=2)

    def save(self, *args, **kwargs):
        if self.total_price < 0:
            raise ValueError("Total price cannot be negative.")
        super().save(*args, **kwargs)  # Call the parent save() method
```

---

### 🔹 Using Model Validators for Field-Level Validation

Django allows built-in or custom **validators** at the field level.

#### ✅ Example: Enforcing Minimum Price
```python
from django.core.validators import MinValueValidator


class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.DecimalField(
        max_digits=10, decimal_places=2, validators=[MinValueValidator(0.01)]
    )
```

---

### 🔹 Using `clean_<field>()` Method

Django provides a `clean_<field>()` method to validate a **specific field**.

#### ✅ Example: Ensuring a Username Doesn't Contain Special Characters
```python
import re


class UserProfile(models.Model):
    username = models.CharField(max_length=150)

    def clean_username(self):
        if not re.match(r"^[a-zA-Z0-9_]+$", self.username):
            raise ValidationError("Username can only contain letters, numbers, and underscores.")
```

---

## Getting Help

###  Where to Find the Documentation?

You can find all Django model field types in the official documentation:  
🔗 [Django Model Field Reference](https://docs.djangoproject.com/en/stable/ref/models/fields/)  

This page contains **all available field types**, along with **their required and optional arguments**.

### Using Python Help to See Field Options
Run this in Python (or Django shell with `python manage.py shell`):
```python
from django.db import models
help(models.CharField)
```
This will show **all available options** for `CharField`.
