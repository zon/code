# Effective Go

*Source document: [Effective Go (go.dev)](https://go.dev/doc/effective_go)*


## Introduction

Go is a new language.  Although it borrows ideas from existing languages, it has unusual properties that make effective Go programs different in character from programs written in its relatives. A straightforward translation of a C++ or Java program into Go is unlikely to produce a satisfactory result—Java programs are written in Java, not Go. On the other hand, thinking about the problem from a Go perspective could produce a successful but quite different program. In other words, to write Go well, it's important to understand its properties and idioms. It's also important to know the established conventions for programming in Go, such as naming, formatting, program construction, and so on, so that programs you write will be easy for other Go programmers to understand.

This document gives tips for writing clear, idiomatic Go code. It augments the language specification, the Tour of Go, and How to Write Go Code, all of which you should read first.

Note added January, 2022: This document was written for Go's release in 2009, and has not been updated significantly since. Although it is a good guide to understand how to use the language itself, thanks to the stability of the language, it says little about the libraries and nothing about significant changes to the Go ecosystem since it was written, such as the build system, testing, modules, and polymorphism. There are no plans to update it, as so much has happened and a large and growing set of documents, blogs, and books do a fine job of describing modern Go usage. Effective Go continues to be useful, but the reader should understand it is far from a complete guide. See issue 28782 for context.


### Examples

The Go package sourcesare intended to serve not only as the core library but also as examples of how to use the language. Moreover, many of the packages contain working, self-contained executable examples you can run directly from the go.dev web site, such as this one (if necessary, click on the word "Example" to open it up). If you have a question about how to approach a problem or how something might be implemented, the documentation, code and examples in the library can provide answers, ideas and background.


## Table of Contents

* [Formatting](formatting.md)
* [Commentary](commentary.md)
* [Names](names.md)
  * [Package names](names_package_names.md)
  * [Getters](names_getters.md)
  * [Interface names](names_interface_names.md)
  * [MixedCaps](names_mixedcaps.md)
* [Semicolons](semicolons.md)
* [Control structures](control_structures.md)
  * [If](control_structures_if.md)
  * [Redeclaration and reassignment](control_structures_redeclaration_and_reassignment.md)
  * [For](control_structures_for.md)
  * [Switch](control_structures_switch.md)
  * [Type switch](control_structures_type_switch.md)
* [Functions](functions.md)
  * [Multiple return values](functions_multiple_return_values.md)
  * [Named result parameters](functions_named_result_parameters.md)
  * [Defer](functions_defer.md)
* [Data](data.md)
  * [Allocation with `new`](data_allocation_with_new.md)
  * [Constructors and composite literals](data_constructors_and_composite_literals.md)
  * [Allocation with `make`](data_allocation_with_make.md)
  * [Arrays](data_arrays.md)
  * [Slices](data_slices.md)
  * [Two-dimensional slices](data_two_dimensional_slices.md)
  * [Maps](data_maps.md)
  * [Printing](data_printing.md)
  * [Append](data_append.md)
* [Initialization](initialization.md)
  * [Constants](initialization_constants.md)
  * [Variables](initialization_variables.md)
  * [The init function](initialization_the_init_function.md)
* [Methods](methods.md)
  * [Pointers vs. Values](methods_pointers_vs_values.md)
* [Interfaces and other types](interfaces_and_other_types.md)
  * [Interfaces](interfaces_and_other_types_interfaces.md)
  * [Conversions](interfaces_and_other_types_conversions.md)
  * [Interface conversions and type assertions](interfaces_and_other_types_interface_conversions_and_type_assertions.md)
  * [Generality](interfaces_and_other_types_generality.md)
  * [Interfaces and methods](interfaces_and_other_types_interfaces_and_methods.md)
* [The blank identifier](the_blank_identifier.md)
  * [The blank identifier in multiple assignment](the_blank_identifier_the_blank_identifier_in_multiple_assignment.md)
  * [Unused imports and variables](the_blank_identifier_unused_imports_and_variables.md)
  * [Import for side effect](the_blank_identifier_import_for_side_effect.md)
  * [Interface checks](the_blank_identifier_interface_checks.md)
* [Embedding](embedding.md)
* [Concurrency](concurrency.md)
  * [Share by communicating](concurrency_share_by_communicating.md)
  * [Goroutines](concurrency_goroutines.md)
  * [Channels](concurrency_channels.md)
  * [Channels of channels](concurrency_channels_of_channels.md)
  * [Parallelization](concurrency_parallelization.md)
  * [A leaky buffer](concurrency_a_leaky_buffer.md)
* [Errors](errors.md)
  * [Panic](errors_panic.md)
  * [Recover](errors_recover.md)
* [A web server](a_web_server.md)


## Ralph Review Configuration

To configure `ralph review` with every Effective Go section as a review item, add the following to your `.ralph/config.yaml` file:

```yaml
review:
  items:
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/formatting.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/commentary.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/names.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/names_package_names.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/names_getters.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/names_interface_names.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/names_mixedcaps.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/semicolons.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/control_structures.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/control_structures_if.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/control_structures_redeclaration_and_reassignment.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/control_structures_for.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/control_structures_switch.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/control_structures_type_switch.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/functions.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/functions_multiple_return_values.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/functions_named_result_parameters.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/functions_defer.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/data.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/data_allocation_with_new.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/data_constructors_and_composite_literals.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/data_allocation_with_make.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/data_arrays.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/data_slices.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/data_two_dimensional_slices.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/data_maps.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/data_printing.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/data_append.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/initialization.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/initialization_constants.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/initialization_variables.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/initialization_the_init_function.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/methods.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/methods_pointers_vs_values.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/interfaces_and_other_types.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/interfaces_and_other_types_interfaces.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/interfaces_and_other_types_conversions.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/interfaces_and_other_types_interface_conversions_and_type_assertions.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/interfaces_and_other_types_generality.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/interfaces_and_other_types_interfaces_and_methods.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/the_blank_identifier.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/the_blank_identifier_the_blank_identifier_in_multiple_assignment.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/the_blank_identifier_unused_imports_and_variables.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/the_blank_identifier_import_for_side_effect.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/the_blank_identifier_interface_checks.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/embedding.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/concurrency.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/concurrency_share_by_communicating.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/concurrency_goroutines.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/concurrency_channels.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/concurrency_channels_of_channels.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/concurrency_parallelization.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/concurrency_a_leaky_buffer.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/errors.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/errors_panic.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/errors_recover.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/go/a_web_server.md
```
