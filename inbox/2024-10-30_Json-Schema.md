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


