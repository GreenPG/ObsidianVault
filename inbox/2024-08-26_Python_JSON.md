---
date: 2024-08-26
tags:
    - #JSON
hubs:
    - "[[Python]]"
    - "[[data_serialization]]"
urls:
    - https://docs.python.org/3/library/json.html
---

# Python_JSON 

Description of the API given by Python built-in "json" module.

## Basic Usage

- ```json.dump(obj, fp, *, skipkeys= False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, **kw)```
Serialize ```obj``` as a JSON formatted stream to ```fp``` (a ```.write()```-supporting file-like-object). The module always produces ```str``` objects, not bytes. There ```fp.write``` must support ```str``` input.

    - skipkeys: if True, dict that are not of basic type (str, int, float, bool, None) will be skipped instead of raisin TypeError.
    - ensure_ascii: if True,  all incoming non-ASCII characters will be escaped, if false, they will be output as-is.
    - check_circular: if false, circular reference check for container types will be skipped and will result in RecursionError.
    - allow_nan: if False, serialization of out of range float values will raise ValueError (in compliance with JSON specification). If true, JS equivalents will be used.
    - indent: if non-negative int or str, array and object JSON elements will be pretty-printed following given indent. Indent level of 0, negative or "" will only insert new line.
                None select the most compact representation. 
    - separators: should be a (item_separator, key_separator) tuple. 
    - default: should be a function that gets called for objects that can't otherwise be serialized. It should return a JSON encodable object or raise TypeError.
    - sort_keys: if True, dictionnaries will be sorted.
    - cls: should be a JSONEncoder used to serialize additional types.


- json.dumps()
Same parameters as dump(). Serialize obj to a JSON formatted str.

- ```json.load(fp, *, cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, **kw)``` 
