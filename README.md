Welcome to unit testing with conan.io TN-TECH blog article demo project
===

Requirements
---
- Modern C++17 compiler
- CMake version >= 3.12
- Boost libraries
- GTest libraries

Demo project scope
---
A lot of people take conan for granted. Yes, it is very powerful C/C++ package manager, yet very few people go deep and exploit it's full power.
The goal of this article is not to showcase the power of conan.io, but to show developers that it is very easy to use when it comes to unit testing.

The idea for this article and demo project came from constant questions by junior colleagues "how do I restrict include and link flags when using conan.io?", "Darn! Conan makes CMake to link all the libraries to the main binary, even ones that I need only for unit tests. How to fix that?", etc.

When it comes to the actual C++ code for this project, the idea is to:
- Create a small library that will convert any input via stream in simplified properties file format (no groups) to JSON format (not pretty printed) and save it via stream.
- Property name can have only letters, numbers and underscores but must start with letter.
- The lines that are ill-formed should be ignored.
- If multiple properties with same name/key are given, the last one will be used.
- Anything is allowed as value, including empty string as long it is in one line.

Sample input:
```text
location=/var/tmp
extension=log
pattern=log-%YYYY%MM%DD
blabla+foo
maxfilesize=16MB
indexlocation=suffix
compress-no
``` 

Sample output:
```json
{
  "location": "/var/tmp","extension": "/log","pattern": "log-%YYYY%MM%DD","maxfilesize": "16MB","indexlocation": "suffix"
}
```

