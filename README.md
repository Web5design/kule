### Simple REST Interface for MongoDB.

Kule is a REST interface for MongoDB that allows you to create simple REST APIs. You can use kule as a temporary backend for your backend needed apps.

### Requirements

 - Bottle
 - pymongo

### Usage

    python -m kule --database foo --collections users,documents

That's all. 

![Kule](http://i.imgur.com/OGeijqr.png)


Now you can iteract with your API. 


| Method        | Path          |           Action              |
| ------------- |---------------| ------------------------------|
| GET           | /users        | Returns all records. You can give limit and offset parameters to paginate records.     |
| GET           | /users/:id    | Returns a single document     |
| POST          | /users        | Creates a new document        |
| PUT           | /users/:id    | Replaces an existing document |
| PATCH         | /users/:id    | Updates a document            |
| DELETE        | /users/:id    | Removes an existing document  |



### Customization

You can customize your API response for your requirements.
For example, you can provide authentication method.

#### Example

You can override an existing method.

```python
from kule import Kule

class MyKule(Kule):
    def delete_detail(self, collection, pk):
        return self.not_implemented()
```

#### get_foo_list, put_foo_detail ...

You can override specific endpoint with kule's magical methods.

```python
from kule import Kule

class MyKule(Kule):
    def get_users_list(self, collection):
        return ["merhaba", "hello", "hola"]
```

#### build_foo_bundle

Also there is a way to build customized bundles.

```python
from kule import Kule

class MyKule(Kule):
    def build_users_bundle(self, user):
        first_name, last_name = user.get("full_name").split()
        return {
            "first_name": first_name,
            "last_name": last_name
        }
```

#### Starting app

```python
from bottle import run
run(app=MyKule(database="foo").get_bottle_app())
```
