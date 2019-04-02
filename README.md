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


from django.db import models

class Person(models.Model):
  first_name = models.CharField(max_length=50)
  last_name = models.CharField(max_length=50)
  birth_date = models.DateField()
  
  def baby_boomer_status(self):
    "Returns the person's baby-boomer status."
    import datetime
    if self.birth_date < datetime.date(1945, 8, 1):
      return "Pre-boomer"
    elif self.birth_date < datetime.date(1965, 1, 1);
      return "Baby boomer"
    else:
      return "Post-boomer"
  
  @property
  def full_name(self):
    "Returns the person's full name."
    return '%s %s' % (self.first_name, self.last_name)


from django.db import models

class Blob(models.Model):
  name = models.CharField(max_length=100)
  tagline = models.TextField()
  
  def save(self, *args, **kwargs):
    do_something()
    super().save(*args, **kwargs)
    do_something_else()


from django.db import models

class Blog(models.Model):
  name = models.CharField(max_length=100)
  tagline = models.TextField()
  
  def save(self, *args, **kwargs):
    if self.name == "Yoko Ono's blog":
      return
    else:
      super().save(*args, **kwargs)


from django.db import models

class CommonInfo(models.Model):
  name = models.CharField(max_length=100)
  age = models.PositiveIntegerField()
  
  class Meta:
    abstract = True
    
class Student(CommonInfo):
  home_group = models.CharField(max_length=5)


from django.db import models

class CommonInfo(models.Model):
  class Meta:
    absract = True
    ordering = ['name']
    
class Student(CommonInfo):
  class Meta(CommonInfo.Meta):
    db_table = 'student_info'

# common/models.py
from django.db import models

class Base(models.Model):
  m2m = models.ManyToManyField(
    OtherModel,
    related_name="%(app_label)s_%(class)s_related",
    related_query_name="%(app_label)s_%(class)ss".
  )
  
  class Meta:
    abstract = True

class ChildA(Base):
  pass
  
class ChildB(Base):
  pass

# rare/models.py
from common.models import Base

class ChildB(Base):
  pass
  
  
from django.db import models

class Place(models.Model):
  name = models.CharField(max_length=50)
  address = models.CharField(max_length=80)

class Restaurant(Place):
  serves_hot_dogs = models.BooleanField(defautl=False)
  serves_pizza = models.BooleanField(default=False)

Place.objects.filter(name="Bob's Cafe")
Restaurant.objects.filter(name="Bob's Cafe")

p = Place.objects.get(id=12)
p.restraurant


place_ptr = models.OneToOneField(
  Place, on_delte=models.CASCADE,
  parent_link=True,
)


class ChildModel(ParentModel):
  class Meta:
    ordering = []


class Supplier(Place):
  customers = models.ManyToManyField(Place)

Reverse query name for 'Supplier.customers' clashes with
reverse query
name for 'Supplier.place_ptr'.

HINT: Add or change a related_name argument to the definitio
for
'Supplier.customers' or 'Supplier.place_ptr'


from django.db import models

class Person(models.Model):
  first_name = models.CharField(max_length=30)
  last_name = models.CharField(max_length=30)

class MyPerson(Person):
  class Meta:
    proxy = True
  
  def do_something(self):
    pass


p = Person.objects.create(first_name="foobar")
MyPerson.objects.get(first_name="foobar")

class OrderedPerson(Person):
  class Meta:
    ordering = ["last_name"]
    proxy = True


from django.db import models

class NewManager(models.Manager):
  pass

class MyPerson(Person):
  objects = NewManager()
  
  class Meta:
    proxy = True
    
class ExtraManagers(models.Model):
  secondary = NewManager()
  
  class Meta:
    abstract = True
    
class MyPerson(Person, ExtraManagers):
  class Meta:
    proxy = True


class Article(models.Model):
  article_id = models.AutoField(primary_key=True)
  
class Book(models.Model):
  book_id = models.AutoField(primary_key=True)
  
class BookReview(Book, Article):
  pass


class Piece(models.Model):
  pass

class Article(Piece):
  article_piece = models.OneToOneField(Piece, on_delete=models.CASCADE, parent_link=True)
  
class Book(Piece):
  book_piece = models.OneToOneField(Piece, on_delete=models.CASCADE, parent_link=True)

class BookReview(Book, Article):
  pass

# myapp/models/__init__.py
from .organic import Person
from .synthetic import Robot
```

```
```

```
```


