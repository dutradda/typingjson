# typingjson

<p align="center" style="margin: 3em">
  <a href="https://github.com/dutradda/typingjson">
    <img src="https://dutradda.github.io/typingjson/typingjson.svg" alt="typingjson" width="300"/>
  </a>
</p>

<p align="center">
    <em>Interoperates <b>@dataclass</b> with <b>json objects</b></em>
</p>

---

**Documentation**: <a href="https://dutradda.github.io/typingjson" target="_blank">https://dutradda.github.io/typingjson</a>

**Source Code**: <a href="https://github.com/dutradda/typingjson" target="_blank">https://github.com/dutradda/typingjson</a>

---


## Key Features

- Full compatibility with [dataclasses](https://docs.python.org/3/library/dataclasses.html) module*
- Deserialize values from dict
- Deserialize values from bytes*
- Deserialization/serialization of choosen fields
- Dict serialization*
- Direct json serialization with [orjson](https://github.com/ijl/orjson) (don't convert to dict before serialization)
- Optional validation according with the [json-schema](https://json-schema.org/) specification*

*\* feature in development.*


## Requirements

 - Python 3.7+
 - [orjson](https://github.com/ijl/orjson) for json serialization (optional, but recommended)


## Instalation
```
$ pip install typingjson[orjson]
```


## Basic example

```python
from dataclasses import dataclass
from typing import List

from typingjson import asdataclass, asjson, typingjson


@dataclass
class Music:
    name: str


@typingjson
@dataclass
class Person:
    name: str
    age: int
    musics: List[Music]


jsondict = dict(name=b'John', age='40', musics=[dict(name='Imagine')])
person = asdataclass(jsondict, Person)

print(person)
print(asjson(person))

```

```
Person(name='John', age=40, musics=[Music(name='Imagine')])
b'{"name":"John","age":40,"musics":[{"name":"Imagine"}]}'

```


## Example for choose fields to deserialize

```python
from dataclasses import dataclass
from typing import List

from typingjson import asdataclass, asjson, typingjson


@dataclass
class Music:
    name: str


@typingjson(deserialize_fields=('name', 'age'))
@dataclass
class Person:
    name: str
    age: int
    musics: List[Music]


jsondict = dict(name=b'John', age='40', musics=[dict(name='Imagine')])
person = asdataclass(jsondict, Person)

print(person)
print(asjson(person))

```

```
Person(name='John', age=40, musics=[{'name': 'Imagine'}])
b'{"name":"John","age":40,"musics":[{"name":"Imagine"}]}'

```


## Example for choose fields to serialize

```python
from dataclasses import dataclass
from typing import List

from typingjson import asdataclass, asjson, typingjson


@dataclass
class Music:
    name: str


@typingjson(serialize_fields=('name', 'age'))
@dataclass
class Person:
    name: str
    age: int
    musics: List[Music]


jsondict = dict(name='John', age=40, musics=[dict(name='Imagine')])
person = asdataclass(jsondict, Person)

print(person)
print(asjson(person))

```

```
Person(name='John', age=40, musics=[Music(name='Imagine')])
b'{"age":40,"name":"John"}'

```


## Wins [Pydantic](https://github.com/samuelcolvin/pydantic) Benchmark

`typingjson` is *2.5 times* faster than pydantic on it's benchmark

![pydantic benchmark](https://dutradda.github.io/typingjson/benchmark.png "Pydantic Benchmark")