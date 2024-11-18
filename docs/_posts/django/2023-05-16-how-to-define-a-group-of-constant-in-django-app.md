---
title: "How to define a group of constant in Django app?"
categories:
  - Django
tags:
  - django
---

![](/assets/images/2023/05/2023-05-how-to-define-a-group-of-constant-in-django-app-cover.webp)

## Group of constants
A group of constants value will help group the constant by specific type or meaning. 

For example, this blog post might have multiple status like draft, publish then we could use a group with named `POST_STATUS` to group all of them together.

## Use cases
In a Django app, I usually use group of constants in two common use cases:

– Define choices for a field in the model

– Use this group of constants in the logic app

## How to define a group of constants?
### Use tuple
You might define each constant type with a name then group them by a tuple, like this:

```python
(POST_DRAFT, POST_PUBLISHED, POST_ARCHIVED) = range(3)
POST_STATUS_CHOICES = (
   (POST_DRAFT, 'Draft'),
   (POST_PUBLISHED, 'Published')
   (POST_ARCHIVED, 'Archived')
)
```

You might want to use this group of constants in a model field choices:

```python
class Post(models.Model):
    post_status = models.IntegerField(
        choices=POST_STATUS_CHOICES,
        default=POST_STATUS_CHOICES[0][0]
    )
```

Above code snippet also show you get the default value is `POST_DRAFT` with 
```python
POST_STATUS_CHOICES[0][0]
```

This way is work but lack of reading on code, where you might forget about the value of the first one then need to re-check on where define the group.

## Use Enum
There is a better way to avoid select by the index of the value as above is using enum value.

Firstly, define a class stand for the choices by enums, and provide a method to get all values by tuple named “choices”
```python
import enum
from enum import Enum

@enum.unique
class EnumChoices(Enum):
    @classmethod
    def choices(cls):
        return [(item.value, item.name) for item in cls]
```

then define a class PostStatus extend from EnumChoices

```python
class PostStatus(EnumChoices):
    POST_DRAFT = 0
    POST_PUBLISHED = 1
finally, use in the model field choices

class Post(models.Model):
    post_status = models.IntegerField(
        choices=PostStatus.choices(),
        default=PostStatus.POST_DRAFT
    )
```

This solution help us avoid the index select by better meaningful name `PostStatus.POST_DRAFT`

### Use Django choices class
Above solution is good to go, but Django makes it even better by already define enum choices class to use, like `IntegerChoices`, `TextChoices`, `Choices`.

Then above code will become:
```python
from django.db.models import IntegerChoices
class PostStatus(IntegerChoices):
    POST_DRAFT = 0
    POST_PUBLISHED = 1
then in model field choices will call to get choices value instead:

class Post(models.Model):
    post_status = models.IntegerField(
        choices=PostStatus.choices,
        default=PostStatus.POST_DRAFT
    )
```

For summary, we should refer the Django choice class since it is the better option for clean code and readable constant value in the group.