---
date: 2024-10-30
tags:
    - #Doc 
hubs:
    - "[[data_serialization]]"
urls:
    - https://json-schema.org/learn/getting-started-step-by-step
---

## Glossary
**instance**: document that is bein validated or described
**schema**: document that contains the description

# Json Schema 

Json Schema is a vocabulary that can be use to annotate and validate JSON documents. 

A schema is a a json file.
The most basic schema is a blank JSON object which contains nothing, therefore allowing anything and describing nothing.

You can apply constraints by adding validataion keywords.

## Creating a schema definition
To create a basic schema definition, define the following keywords:
- **$schema**: specifies which draft of the JSON Schema standard the schema adheres to
- **$id**: set a unique URI for the schema. Can be used to refer to elements of the schema from inside the same doc, or from external JSON docs.
- **title** and ** **description**: state the intent of the schema. Don't add constraints to the data being validated
- **type**: defines the first constrain on the JSON data. **type** can take the following values: object, array, string, number, boolean or null.

Keywords are defined using JSON keys. The datas validated are typically contained in JSON data doc, but JSON schema can also validate JSON data contained in other document type.

## Define properties

**properties** keywords is used to defines keys of an object in the JSON data that's being validated. You can also defined which one is required.
To add the **properties** of an object, add the **properties** keyword at the end of an object schema, then add the keys with the following schema annotations:
- *description*: describe what the key is.
- *type*: define what kind of data is expected.
Ex:
```
{
    "title": "Product",
    "description": "A product",
    "type": "object",
    "properties": {
        "productId": {
            "description": "The unique identifier of a product",
            "type": "integer"
        }
    }
}
```

## Define required properties

You can define required properties in a schema.
To do it, add the **required** keyword to the end of an object, after the properties. It's a list in which you can put the id of the properties you want to be mandatory.

## Type specific properties

Some types have specific properties that can be used to constraints the value/contents of the data.
Those has to be placed inside the data definition. 

### Numbers
Numbers can have a specified range with the following keyword:
 - *minimum*
 - *exclusiveMinimum*
 - *maximum*
 - *exclusiveMaximum*

### Strings

#### Length
The length of string can be consrtained with *minLength* and *maxLength*. Both takes a non-negative number as value.

#### Regular expression
The *pattern* keyword can be used to constraints a string to a particular regex following syntax define in JS.

#### Format
The *format* keyword allow for basics semantic identification of certain kind of strings values commonly used.
List of the built-in's formats:
 -  Dates and times:
    - "date-time": date and time together
    - "time"
    - "date"
    - "duration": duration as defined by  [ISO 8601 ABNF for "duration"][https://datatracker.ietf.org/doc/html/rfc3339#appendix-A] 
-   Email addresses:
    - "email"
    - "idn-email"
- Hostnames:
    - "hostname"
    - "idn-hostname"
- IP addresses:
    - "ipv4"
    - "ipv6"
- Resource identifiers
    - "uuid"
    - "uri"
    - "uri-reference"
    - "iri"
    - "iri-reference"
- URI template
    - "uri-template"
- JSON Pointer
    - "json-pointer"
    - "relative-json-pointer"
- Regular expression
    - "regex"

### Arrays

List are generally used in two ways in JSON:
- *List validation*: a sequence of arbitrary length where each item matches the same schema
- *Tuple validation*: a sequence of fixed length where each item may have differ schema. In this case, the index of each items is meaningful as how to the value in interpreted.

#### Items

For a list validation usage, set the **items** keyword to a single schema that will be used to validate all of the items in the array. Ex for an array of number:
```
{
    "type": "array",
    "items": {
        "type": "number"
    }
}
```

#### Tuple validation

For a tuple validation usage, use the **prefixItem** keyword. It's an array where each item is a schema that corresponds to each index of the doc's array.
Ex:
```
{
    "type": "array",
    "prefixItems": [
        { "type": "number" },
        { "type": "string" },
        { "enum": ["Street", "Avenue", "Boulevard"] },
        { "enum": ["NW", "NE", "SW", "SE"] },
    ]
}
```
validates =  ```[1600, "Pennsylvanua", "Avenue", "NW]```

##### Additional items
The **items** keyword can be used to control wheter it's valid or not to have additonal items in a tuple beyond those defined in **prefixItems**. It has the same format as for a list validation, but you can also set its value to 'false', disallowing extra items in the tuple.




#### Unevaluated items

The **unevaluatedItems** keyword is useful when you want to add or disallow extra item to an array.
It applies to any values not evaluated by **items** or **prefixItem**, or **contains**.
It affect only items in an array.
If you set it to "false", you can disallow extra items for array.

#### Contains 

Unlike **items**, **contains** schema only need to validate agains one or more items in the array. Ex:
This schema:
```
{
    "type": "array",
    "contains": {
        "type": "number"
    }
}
```
validates this array: ```["life", "univers", "everythin", 42]```, but fails for : ```["life", everything", "universe", "forty-two"]```

#### minContains/maxContains

**minContains** and **maxContains** can be used with **contains**to further specify how many times schema matches a **contains** constraint. Those can only be non-negative numbers.

#### Length

The length of an array can be specified using **minItems** and **maxItems** keywords. They can only take non-negative number.

#### Uniqueness

A schema can ensure that each of the items in an array is unique by simply set **uniqueItmes** keyword to "true".


### Object

JSON Schema objects are analogous to *dict* in Python, *Hash* in Ruby, *NSDictionnary* in Objective-C or *Dictionnary* in Swift.

#### Pattern Properties

**patternProperties** keyword can be used to define properites with names that follow specific patterns using regex.
Regular expressions are not anchored, so a patternProperties as "p" will mathc any property containing a "p", not just property whose named "p".
It's usually less confusing to surround the regex in ^...$, (ex: ^p$)

#### Additional Properties

#### Extending Closed Schemas

#### Unevaluated Properties

#### Required Properties

#### Property Names

#### Size

