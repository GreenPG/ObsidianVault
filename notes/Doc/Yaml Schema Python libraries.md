---
date: 2024-06-05
tags:
    - Doc
hubs:
    - "[[Python]]"
    - "[[data_serialization]]"
urls:
    -
---
# Yaml Schema Python libraries 

## Objectif: 
Compare differents Python libraries to validate YAML Schema (structure of the file)


### Schema
Library to validate Python data structure converted from JSON or Yaml. 
Pretty simple to use.
Schema() class that take as arguments the structure of the intended data input, written like you write Python data structure using types.
Possibility to use personal class, but used after the data as been converted from Yaml to Python, so the parser should have seen an error before.
Possibility to use regex or custom checking function.


### Cerberus
Possibilities comparable to Schema, but seems less readable.
Must too be used after yaml parsing.
Dont raise exception at first validation error, but always process the entire document and return False if the validation failed.

### Yamale
Validate and convert yaml to python.
Possibility to chose between PyYaml or ruamel as parser.

Schema based on Yaml file or 'stringified yaml'. Have schema written in plain Yaml could be practical for config file author.
Possibility to create custom validator, but is bit complicated for complex class.
Cannot validate custom classes, by using ruamel to parse it for example.


### Pydantic
Data validation library, where validation means: instantiate a model that adhere to specified types and constraint, not only verify that the data
correspond to specified schema.

Have a pydantic-yaml plugin to hand Yaml that is based on ruamel.yamel. But it don't specify personal yaml loader to parse yaml file,  so there's no possibility to convert the yaml directly in custom Python class.
only to dump to yaml. So not really adapted for the project.
Could still be useful to generate yaml. 

### Yatiml:
Library that can validate yaml data after loading it or before dumping it.
Specificity is that it based is validation on python class and convert it directly to it.
Also a possibility to precise string with custom rule.
Very complete error message.
