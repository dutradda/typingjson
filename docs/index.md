# jsondaora

<p align="center" style="margin: 3em">
  <a href="https://github.com/dutradda/jsondaora">
    <img src="https://dutradda.github.io/jsondaora/jsondaora.svg" alt="jsondaora" width="300"/>
  </a>
</p>

<p align="center">
    <em>Interoperates <b>dataclasses</b> and <b>TypedDict</b> with <b>json objects</b></em>
</p>

---

**Documentation**: <a href="https://dutradda.github.io/jsondaora" target="_blank">https://dutradda.github.io/jsondaora</a>

**Source Code**: <a href="https://github.com/dutradda/jsondaora" target="_blank">https://github.com/dutradda/jsondaora</a>

---


## Key Features

- Full compatibility with [dataclasses](https://docs.python.org/3/library/dataclasses.html) module and [TypedDict](https://www.python.org/dev/peps/pep-0589/) annotation
- Deserialize values from dict
- Deserialize values from bytes*
- Deserialization/serialization of choosen fields
- Dict serialization
- Direct json serialization with [orjson](https://github.com/ijl/orjson) (don't convert to dict before serialization)
- Optional validation according with the [json-schema](https://json-schema.org/) specification*

*\* feature in development.*


## Requirements

 - Python 3.8+
 - [orjson](https://github.com/ijl/orjson) for json serialization


## Instalation
```
$ pip install jsondaora
```


## Basic example

```python
{!./src/index/index_00_basic.py!}
```

```
{!./src/index/index_00_basic.output!}
```


## Example for choose fields to deserialize

```python
{!./src/index/index_02_deserialize_fields.py!}
```

```
{!./src/index/index_02_deserialize_fields.output!}
```


## Example for choose fields to serialize

```python
{!./src/index/index_03_serialize_fields.py!}
```

```
{!./src/index/index_03_serialize_fields.output!}
```


## Wins [Pydantic](https://github.com/samuelcolvin/pydantic) Benchmark

`jsondaora` is up to *5.6 times* faster than pydantic on it's benchmark

![pydantic benchmark](https://dutradda.github.io/jsondaora/benchmark.png "Pydantic Benchmark")