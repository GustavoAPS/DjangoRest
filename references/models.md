# Models 

Models are the database layout of Django with additional metadata.

# Introduction

- [Simple Model](#simple-model)
- [Model Fields](#model-fields)
- [Getting Help](#getting-help)

## Simple model

The most simple way to create a model in Django is to create a class that that subclasses django.db.models.Model

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
