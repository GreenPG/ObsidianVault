---
date: 2024-06-18
tags:
    -
hubs:
    "[[]]"
urls:
    -
---
# Protocol Buffers 

Protocol Buffers are a language-neutral, platform-neutral extensible mechanism for serializing structured data.
Provide a serialization format for packets of typed, structured data that are up to a fiew Mb in size. Suitable for ephemeral network traffic and long term data storage.
Advantages of Protocol Buffers:
- Compact data storage
- Fast parsing
- Availability in many programming languages
- Optimized functionnality through automatically-generated classes

Protocol Buffers are not a good fit when:
- Data exceending a few Mb.
- Comparing two messages without parsing them
- uses that involve large, multi-dimensional arrays of floating point.
- with non-OOP languages popular in scientific computing (ex: Fortran, IDL)
- you cannot fully interpret PB messages without access to it's correspond .proto file.

![[Pasted image 20240618143948.png]]:w
Protocol Buffers workflow

## PB Definition Syntax

You can defined that a field is either optional, repeated or leave to the default implicit presence.
You then specify the field data type, which can be usual primitive types, or PB specific types:
- message: allow to nest parts of the definition, for repeating sets of data
- enum
- oneof: when a message has many optional and only one of them will be set
- map

Then you choose a name for the field, which cannot contain dashes. Convention to use pluriral names for repeated
fields.
Finally you assign a number to the field, which cannot bie repurposed of reused.

