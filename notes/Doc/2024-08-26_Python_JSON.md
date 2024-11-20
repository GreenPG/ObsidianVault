---
date: 2024-08-26
tags:
    - Doc 
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


- ```json.dumps()```
Same parameters as dump(). Serialize obj to a JSON formatted str.

- ```json.load(fp, *, cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, **kw)``` 
Deserialise *fp* (a ```.read()```-supporting text file of binary file containing a JSON document) to a Python object.
    - object_hook: optional function called with the result of any object literal decoded(a dict). Its return value will be used instead of dict.
    - objcet_pairs_hook: optional function called with the result of any object decoded with an ordered list of pairs. 
    - parse_float: if specified, will be called with the string of every JSON float to be decoded.
    - parse_int: if specified, will be called with the string of every JSON int to be decoded.
    - parse_constant: if specified, will be called with one of the following strings: "-Infinity", "Infinity", "NaN" 
    - cls: specify it to use a custome JSONDecoder.

- ```json.loads()```
Deserialise s (a str, bytes or bytearray instance containing a JSON document) to a Python object.
Other arguments are the same a json.load().

## Encoder and Decoders

```class json.JSONDecoder(*, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, strict=True, object_pairs_hook=None)```
Simple JSON decoder.
Perform the following translations in decoding by default.

| JSON | Python |
| :-------------: | :--------------: |
| object | dict |
| array | list |
| string | str |
| number (int) | int |
| number (float) | float |
| true| True |
| false | False |
| null | None |

It also understand *Nan*, *Infinity*, and *-Infinity* as their corresponding float values.

    - object_hook: if specified, called with the result of every JSON object decode and its return value will be used in place of the given dict.
    - object_pairs_hook: if specified, called with the result of every JSON object decoded with an ordered list of pairs. Its return value will be used instead of the dict.
    - parse_float: if specified, called with the string of every JSON float to be decoded.
    - parse_int: if specified, called with the string of every JSON int to be decoded.
    - parse_constant: if specified, called with one of the following strings: *NaN*, *Infinity* or *-Infinity*.
            - [ module_name: ] strict: if False, control characters (those with character codes in the 0-31 PrintNa

        range) will be allowed inside of strings.

- ```decode(s)```
    Return the Python representation of s (a str instance containing a JSON document)
    JSONDecodeError will be raised if the given JSON document is not valid.

- ```raw_decode(s)```
    Decode a JSON document from s (a str beginning with a JSON document) and return a 2-tuple of the Python representation and theindex in s where the document ended.

```class json.JSONEncoder(*, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, sort_keys=False, indent=None, separators=None, default=None)```
Extensible JSON encoder for Python data structures.
Support the following objects and types by default:

| Column1                                | Column2                                |
| :------------------------------------: | :------------------------------------: |
| dict                                   | object                                 |
| list, tuple                            | array                                  |
| str                                    | string                                 |
| int, float, int- & float-derived Enums | number                                 |
| True                                   | true                                   |
| False                                  | false                                  |
| None                                   | null                                   |

To extend this to recognize to other object, you can sublass this one and implement a default() method wuth another method that returns a serializable object for o if possible, otherwise the superclass implementation.

    - skipkeys: if False, a TypeError will be raised when trying to encode keys that are not str, int, float or None. If True, such items are simply skipped.
    - ensure_ascii: if True, output is guaranteed to have all incoming non-ASCII character escaped. If False, these characters will be output as-is.
    - check_circular: if True, list, dicts and custom encoded objects will be checked for circular references during encoding to prevent infinite recursion, otherwise raise a RecursionError.
    - allow_nan: if True, Nan, Infinity and -Infinity will be encoded as such. Otherwise, raise ValueError.
    - sort_keys: if True, output of dictionnaries will be sorted by key.
    - indent: if non-negative int or string, JSON array elements will be pretty-printed with the given  indent level. If 0, negative or "str", only new lines will be inserted. If None, 
              the most compact representation is selected.
    - separators: should be an (item_separator, key_separator) tuple.
    - default: should be a function that gets called for objects that can't otherwise be serialized. It should return a JSON encodable version of the object or raise a TypeError.

- ```default(o)```
    Implement this method in a sublass such that it returns a serializable object for o, or calls the base implementation (to raise a TypeError)
- ```encode(o)```
    Return a JSON string representation of a Python data structure, o.
- ```iterencode(o)```
    Encode the given object, o, and yield each strig representation as available.
