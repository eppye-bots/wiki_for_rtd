  1. bots 3.2.0 is suited for django 1.4, 1.5 and 1.6. Support for Django 1.3 is dropped.
  1. in existing settings.py django requires parameter 'ALLOWED\_HOSTS'. Add this as eg:
```
    ALLOWED_HOSTS = ['*']
```