### django-models
---
https://docs.djangoproject.com/en/dev/topics/db/models/

```py
from django.db import models

class Person(models.Model):
  first_name = models.CharFields(max_length=30)
  last_name = models.CharField(max_length=30)

CREATE TABLE myapp_person (
  "id" serial NOT NULL PRIMARY KEY,
  "first_name" varchar(30) NOT NULL,
  "last_name" varchar(30) NOT NULL
);

INSTALLED_APPS = [
  'myapp',
]








































```

```
```

```
```


