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
Finally you assign a number to the field, which cannot bie repurposed of reused. It's an unique tag used by
the field to realize the binary encoding.

Exemple of a simple adress book .proto file:
```
syntax = "proto2";

package tutorial;

message Person {
  optional string name = 1;
  optional int32 id = 2;
  optional string email = 3;

  enum PhoneType {
    PHONE_TYPE_UNSPECIFIED = 0;
    PHONE_TYPE_MOBILE = 1;
    PHONE_TYPE_HOME = 2;
    PHONE_TYPE_WORK = 3;
  }

  message PhoneNumber {
    optional string number = 1;
    optional PhoneType type = 2 [default = PHONE_TYPE_HOME];
  }

  repeated PhoneNumber phones = 4;
}

message AddressBook {
  repeated Person people = 1;
}
```

To implement this data structure in your project, you have to compile the .proto file the desired language.
You do that using protoc CLI. Example for Python:
```
protoc -I=SRC_DIR --python-out=DST_DIR SRC_DIR/filename.proto
```
You can then include it in your programming following the language method.
