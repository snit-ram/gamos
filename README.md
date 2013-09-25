gamos
=====

Gamos is an ORM for nodejs


Mapping API
===========

Just a draft for better undestanding Filtering API

```js
var db = ... //connect;

var Project = gamos.Model.define('Project', {
  title: gamos.dataTypes.STRING,
  description: gamos.dataTypes.TEXT
});

var Task = gamos.Models.define('Task', {
  title: gamos.dataType.STRING,
  description: gamos.dataTypes.TEXT,
  deadline: {
    type: gamos.dataTypes.DATE,
    validation: function (value) {
      return isDate(value);
    }
  },
  project: Project
});
```
Alternatively:
```js
var Project = gamos.Model.define('Project', {
  title: gamos.dataTypes.STRING,
  description: gamos.dataTypes.TEXT
}, {
  hasMany: Task
});
```


Filtering API
=============

For filtering data, I believe we have two big and well defined apis to follow, unless you can come up with something better.


== Django Inspired ==

Operators are written in the form `{field}__{operator}`

```js
    Task.objects.filter({
        deadline__gt: Date.now()
    }).then(function (tasks) {
        //
    });
```


== Mongo Inspired ==

Operators are written in the sub-objects

```js
    Task.objects.filter({
        deadline: {
            $gt: Date.now()
        }
    }).then(function (tasks) {
        //
    });
```

