---
Title: Yaml Schema Python libraires
Date: 2024-06-05
Tags: #Dev #Python #YAML #Testlab
---

## Objectif: 
Compare differents Python libraries to validate YAML Schema (structure of the file)


### Schema
Library to validate Python data structure converted from JSON or Yaml. 
Pretty simple to use.
Schema() class that take as arguments the structure of the intended data input, written like you write Python data class using types.
Possibility to use persona class, but used after the data as been converted from Yaml to Python, so the parser should have seen an error before.


### Pydantic
Data validation library, where validation means: instantiate a model that adhere to specified types and constraint, not only verify that the data
correspond to specified schema.

Have a pydantic-yaml plugin to hand Yaml that is based on ruamel.yamel. But it don't specify personal yaml loader to parse yaml file, 
only to dump to yaml. So not really adapted for the project.
Could still be useful to generate yaml. lg

### Yamale



### Yatiml


### Cerberus
Possibilities comparable to Schema, but seems less readable.
Must too be used after yaml parsing.
