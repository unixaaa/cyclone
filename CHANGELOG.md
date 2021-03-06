# Next Release (tentatively 0.3.1) - Date TBD

TODO: more performance improvements
TODO: SRFI 113

Features:

- Thanks to ecraven, added R7RS function `exact-integer-sqrt` to `(scheme base)`.
- Allow the reader to recognize `+inf.0`, `-inf.0`, `+nan.0`, and `-nan.0`.
- Allow `cond-expand` to test for whether a library exists using the form `(library {library name})`.

Bug Fixes

- Only throw a divide by zero error for integer division. Floating point divide by zero is allowed and evaluates to `nan`.
- Modified SRFI 106 to be smarter about compiling `AI_V4MAPPED` and `AI_ALL`, which are not defined on OpenBSD.

# 0.3 - October 22, 2016

Features:

- Improve performance by inlining numeric arithmetic and comparison operations.
- Reverted `assq`, `assv`, `memq`, and `memv` back to primitives for improved performance. In addition the compiler was modified to allow for more efficient compilation of `assoc` and `member`.
- Improved library support to recognize all of the import set forms: `only`, `except`, `prefix`, and `rename`.
- Allow explicit renaming macros to be declared interactively. This is the first limited support for calling `define-syntax` from `eval`. 
- Added the `get-environment-variables` function from R7RS.
- Added support for the following SRFI's:

     - SRFI 106: A basic socket interface
     - SRFI 128: Comparators

Bug Fixes

- Improved macro hygiene support to properly rename temporary variables in the `let-values` macro.
- Improve output of `error` by using `write` to output objects as they are represented in memory.
- Check for duplicate lambda parameters during compilation.
- Fixed an error that was being raised when calling `(random-source-randomize! default-random-source)` when using SRFI 27.
- Raise an error if `list->string` encounters a list element that is not a character.

# 0.2 - September 7, 2016

Features:

- Added the following libraries from R7RS-large red edition (data structures):
    - SRFI 1 list library
    - SRFI 133 vector library
    - SRFI 111 boxes
    - SRFI 117 mutable queues
    - SRFI 132 sorting library
- Added SRFI 2, `and-let*`
- Added `parameterize` from section 4.2.6 of R7RS to the `(scheme base)` library.
- Added ` let-values` and ` let*-values` to `(scheme base)`.
- Added `infinite?`, `finite?`, and `nan?` to `(scheme inexact)`.
- Added string ports to `(scheme base)` - `open-input-string`, `open-output-string`, and `get-output-string`.
- Added bytevector ports to `(scheme base)` - `get-output-bytevector`, `open-input-bytevector`, and `open-output-bytevector`.
- Modified `cyclone` to also search the current working directory for built-in headers and libraries.

Bug Fixes:

- Thanks to Mark Meyer, identified and fixed several segfaults in `write` and `display`. 
- Updated `write` to display escaped character sequences (EG: `\t`) instead of literal characters.
- Prevent C compilation errors when building a program that only contains basic primitives or a constant at the top level.
- Fixed the compiler to allow application of a function that can take any number of arguments. For example:

         ((lambda test (write test)) 1 2 3 4)

- Updated `eval` to handle functions that take an optional number of arguments.
- Updated `number->string` to omit leading zeros for binary conversions.
- Fixed `apply` to use the proper semantics when receiving more than one data argument.
- Changed the `assoc` and `member` functions to accept an optional comparison function, and modified both families of functions to be native Scheme functions instead of C primitives.
- Allow libraries to contain multiple `import`, `begin`, and `export` sections.
