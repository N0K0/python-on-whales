# Docker builders

The Buildx builders objects.

Don't use the constructor directly. Instead use 
```python
from python_on_whales import docker

my_builder = docker.buildx.inspect("my-builder")

# or

my_builder = docker.buildx.create()

```
For type hints, use this

```python
from python_on_whales import Builder
```

## Attributes

It attributes are the same that you get with the command line:
`docker buildx inspect ...`

Only a few are available at the moment
```
In [1]: from python_on_whales import docker

In [2]: my_builder = docker.buildx.create()

In [4]: def super_print(obj):
   ...:     print(f"type={type(obj)}, value={obj}")
   ...:

@INSERT_GENERATED_CODE@
```

## Methods

{{autogenerated}}
