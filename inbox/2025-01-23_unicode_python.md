---
date: 2025-01-23
tags:
    - Doc
hubs:
    - "[[Python]]"
    - "[[Encoding]]"
urls:
    - https://docs.python.org/3/howto/unicode.html
---

# unicode_python 

Unicode is a specification that aims to list every character used by human languages and give each one its unique code.
A character is the smallest possible component of a test.
Unicode standard describe how chararcters are represented by **code points**. A code point value is an interger in the range 0 to 0x10FFFF ~1.1 million values).
A character is noted U+<code point>.

## Encondings

A Unidode string is a sequence of code points. This sequence needs to be represented in memory as a set of **code units** which are then mapped to 8-bit bytes. 
The rule for translating a Unicode string into a sequence of bytes are called **character encoding** or just an **encoding**.

The most commonly used encodings is UTF-8 and is often used as default by Python. UTF stands for 'Unicode Transformation Format' and the 8 means that 8-bit values are used in the encodings.
UTF-8 has several convenient properties:
    - can handle any Unicode point
    - a Unicode string 

- [ ] 
