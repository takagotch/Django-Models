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


from django.db import models

class Musician(models.Model):
  first_name = models.CharField(max_length=50)
  last_name = models.CharField(max_length=50)
  instrument = models.CharField(max_length=100)
  
class Album(models.Model):
  artist = models.ForeignKey(Musician, on_delete=models.CASCADE)
  name = models.CharField(max_length=100)
  release_date = models.DateField()
  num_stars = models.IntegerField()


YEAR_IN_SCHOOL_CHOICES = (
  ('FR', 'Freshman'),
  ('SO', 'Sophomore'),
  ('JR', 'Junior'),
  ('SR', 'Senior'),
  ('GR', 'Graduate')
)

from django.db import models

class Person(models.Model):
  SHIRT_SIZES = (
    ('S', 'Small'),
    ('M', 'Medium'),
    ('L', 'Large')
  )
  name = models.CharField(max_length=60)
  shirt_size = models.CharField(max_length=1, choices=SHIRT_SIZES)


p = Person(name="Fred Flintstone", shirt_size="L")
p.save()
p.shift_size

p.get_shift_size_display()


from django.db import models

class Fruit(models.Model):
  name = models.CharField(max_length=100, primary_key=True)

fruit = Fruit.objects.create(name='Apple')
fruit.name = 'Pear'
fruit.save()
Fruit.objects.values_list('name', flat=True)


id = models.AutoField(primary_key=True)

first_name = models.CharField("person's first name", max_length=30)

first_name = models.CharField(max_length=30)

poll = models.ForeignKey(
  Poll,
  on_delete=models.CASCADE,
  verbose_name="the related poll",
)
sites = models.ManyToManyField(Site, verbose_name="list of sites")
place = models.OneToField(
  Place,
  on_delete=models.CASCADE,
  verbose_name="related place",
)


from django.db import models

class Manufacturer(models.Model):
  pass
  
class Car(models.Model):
  manufacturer = models.ForeignKey(Manufacturer, on_delete=models.CASCADE)

class Car(models.Model):
  company_that_makes_it = models.ForeignKey(
    Manufacturer,
    on_delete=models.CASCADE,
  )

from django.db import models

class Topping(models.Model):
  pass

class Pizza(models.Model):
  toppings = models.ManyToManyField(Topping)


from django.db import models

class Person(model.Model):
  name = model.CharField(max_length=128)

  def __str__(self):
    return self.name
    
class Group(models.Model):
  name = models.CharField(max_length=128)
  members = models.ManyToManyField(Person, through='Membership')

  def __str__(self):
    return self.name

class Membership(models.Model):
  person = models.ForeignKey(Person, on_delete=models.CASCADE)
  group = models.ForeignKey(Group, on_delete=models.CASCADE)
  date_joined = models.DateField()
  invite_reaseon = models.CharField(max_length=64)


ringo = Person.objects.create(name="Ringo Starr")
paul = Person.objects.create(name="Paul McCartney")
beatles = Group.objects.create(name="The Beatles")
m1 = Membersip(person=ringo, group=beatles, date_joined=date(1962, 8, 16), invite_reaseon="Needed a new drummer.")
m1.save()
beatles.members.all()
ringo.group_set.all()
m2 = Membership.objects.create(person=paul, group=beatles, date_joined=date(1960, 8, 1), invite_reason="Wanted to form a band.")

beatles.mebers.add(joh, through_defaults={'date_joined': date(1960, 8, 1)})
beatles.members.create(name="George Harrison", through_defaults={'date_joined': date(1960, 8, 1)})
beatles.members.set([john, paul, ringo, george], through_defaults={'date_joined': date(1960, 8, 1)})

beatles.members.add(john, through_defaults={'date_joined': date(1960, 8, 1)})
beatles.members.create(name="George Harrison", through_defaults={'date_joined': date(1960, 8, 1)})
beatles.members.set([john, paul, ringo, george], through_defaults={'date_joined': date(1960, 8, 1)})

Membership.objects.create(person=ringo, group=beatles, date_joined=date(1968, 9, 4),
  invite_reason="You've been gone for a month and wee miss you.")
beatles.members.all()
beatles.members.remove(ringo)
beatles.members.all()


beatles.members.clear()
Membership.objects.all()

Group.objects.filter(members__name__startswith='Paul')

Person.objects.filter(
  group_name='The Beatles',
  membership__date_joined__gt=date(1961,1,1))


ringos_membership = Membership.objects.get(group=beatles, person=ringo)

ringo_membership.date_joined
ringos_membership.invite_reason


ringo_membership = Membership.objects.get(group=beatles, person=ringo)
ringos_membership.date_joined
ringos_membership.invite_reason

ringos_membership = ringo.membership_set.get(group=beatles)
ringos_membership.date_joined
ringos_membership.invite_reason

from django.db import models
from geography.models import ZipCode

class Restaurant(models.Model):
  zip_code = models.ForeignKey(
    ZipCode,
    on_delete=models.SET_NULL,
    blank=True,
    null=True
  )

class Example(models.Model):
  pass = models.IntegerField()
  
class Example(models.Model):
  foo__bar = models.IntegerField()


from django.db import models

class 0x(models.Model):
  horn_length = models.IntegerField()
  
  class Meta:
    ordering = ["horn_length"]
    verbose_name_plural = "oxen"


from d

















```

```
```

```
```


