# Django Style Guide

Guidelines to write an awesome Django project!

## Recommended Apps

DRY! Django has many apps available, and a lot of them can help you to develop
your project in a cleaner and faster way. Here we created a curated list
of Apps that can help you:


### Form related

  1. [django-crispy-forms](http://django-crispy-forms.readthedocs.io/en/latest/)
  1. [django-autocomplete-light](https://django-autocomplete-light.readthedocs.io/en/master/)
  1. [django-localflavor](https://django-localflavor.readthedocs.io/en/latest/)

### List related

  1. [django-tables2](https://django-tables2.readthedocs.io/en/latest/)
  1. [django-filter](https://django-filter.readthedocs.io/)

### Static files related

  1. [django_compressor](https://django-compressor.readthedocs.io/)
  1. [django-static-precompiler](https://django-static-precompiler.readthedocs.io/en/stable/)

### General Apps

  1. [django-password](https://github.com/dstufft/django-passwords)
  1. [django-auditlog](https://github.com/jjkester/django-auditlog)
  1. [django-simple-menu](https://django-simple-menu.readthedocs.io/)
  1. [django-annoying](http://skorokithakis.github.io/django-annoying/)

### Debug and CLI

  1. [django-extensions](https://django-extensions.readthedocs.io/)
  1. [IPython](https://ipython.org/)

## URLs

URLs names for simple `models` should follow this format:

`{app_name}_{model_name}_{action}`

Default actions are:
 * `add`: for object creation page
 * `list`: for listing the model's objects
 * `change`: to change a model's object
 * `delete`: to change a model's object
 * `view`: to view a model's object information

## Permissions

Permissions should follow this format:

`{action}_{model}`

And the verbose name for the permission should use `verbose_name` or `verbose_plural_name` defined

If a permission is used too often (like a `view` permission),
you can create an abstract Meta class with this permission as
default, and inherit from it on your model's Meta:

```python
from django.db import models

class ViewMeta:
    default_permissions = ('add', 'change', 'delete', 'view')

class Foo(models.Model):
    class Meta(ViewMeta):
        # Other meta configurations
        verbose_name = "Foo"
        verbose_name_plural = "Foos"
        ordering = ["-id"]
        permissions = []

    # fields definition
```


## Models

All models should have a `Meta` class, and at least
those fields should be defined (in this order) on the Meta
(even if they are empty or follow default Django behaviour):
  1. `verbose_name`
  2. `verbose_plural_name`
  3. `ordering`
  4. `permissions`

Meta class should be defined at the beginning of the class, which allows
ou to get an overview of the Model without scrolling the code. You
must have one blank line between the Meta definition and the fields
definition

All fields must have a `verbose_name`


```python
from django.db import models

class Foo(models.Model):
    class Meta:
        verbose_name = "Foo"
        verbose_name_plural = "Foos"
        ordering = ["-id"]
        permissions = [('move_foo', "Move {}"), ]

    field1 = models.CharField(max_length=255, verbose_name="Field 1")
    field2 = models.Integer(verbose_name="Field 2")
```
