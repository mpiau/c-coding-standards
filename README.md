C Coding Standards
====================

These guidelines are based on my own preferences and experiences.\
You can use them as you like on your personal projects, or adjust them to your needs.

The most important rule to follow when programming is to be *consistent* with the
codebase you are working on. A significant part of writing good code is following
the adopted style and guidelines of the project.
Consistent naming, formatting, ordering, and logic makes it easier to understand each other.
It also helps us to focus on what the code does, which can prevent errors from being overlooked during reviews.


> [!CAUTION]
> This document is in Work-In-Progress: Nothing is finished, everything is poorly written.\
> At this stage, it's mostly a brain dump, but making this repository public motivates me to work on it.


Getting started
---------------

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in RFC 2119.


Not exhaustive TODO List
----------
- [ ] Write an introduction
- [ ] Write a summary
- [ ] Write an indentation section
- [ ] Write a preprocessor section
- [ ] Write a comments section
- [ ] Write a define section
- [ ] Write a formatting section
- [ ] Write a struct / union / enum section
- [ ] Write a header files section
- [ ] Write an implementation file section
- [ ] Write a good naming section
- [ ] Write a "Function" section
- [ ] Write a logic flow section
- [ ] Write a constant section
- [ ] Write a compiler warnings section
- [ ] Write a C recommended version section
- [ ] Write a code organization section
- [ ] Finish the list of this todo-list

# C Programming Language Coding Standards

C-FMT-XX - C Formatting Rules
==

C-FMT-01 - Each line shall be limited to 99 characters
--

A line of code shall not be larger than 99 characters.<br/>
Exceeding this limit often makes the code less readable and artificially increases its complexity.<br/>
A statement exceeding that limit shall be broken into smaller pieces, with the correct alignment.<br/>

```c
// Non compliant example
variable = (ComplexStructure) { .firstString = "A small line of example", .secondString = "Another line of example" };

// Compliant example
variable = (ComplexStructure) {
   .firstString = "A small line of example",
   .secondString = "Another line of example"
};
```

C-FMT-02 - Spaces shall be used for indentation
--

Indentations shall only be done with spaces, not tabs.<br/>

C-FMT-03 - Indentations shall be 3 characters wide
--

Each indentation shall be made with 3 spaces.


C-FMT-TODO - 
--


C-FUNC-XX - C Functions Rules
==

C-FUNC-XX - A function name shall be written in snake_case
C-FUNC-XX - A function shall have at most 4 parameters
C-FUNC-XX - A function with no parameter shall have a `void` parameter.

```c
void non_compliant_function();

void compliant_function( void );
```

C-FUNC-XX - A static function shall be only defined in a .c file.
C-FUNC-XX - Static functions shall only be used within the file they are defined.
C-FUNC-XX - Static functions shall be defined before non-static functions.

C-FUNC-XX - An unused function shall be either disabled by the preprocessor or deleted.
C-FUNC-XX - A non-static function definition shall have its associated declaration in a header file.

C-FUNC-XX - A non-void function shall have at least one return statement
C-FUNC-XX - A non-void function shall have a return statement at the end of the function
C-FUNC-XX - The return value of a function shall either be used or explicitly discarded

C-FUNC-XX - Function attributes and specifiers shall be written in a separated line
```c
[[nodiscard]] static u64 non_compliant_function( void )
{
   [...]
}


[[nodiscard]] static
u64 compliant_function( void )
{
   [...]
}
```

C-FUNC-XX - Attributes shall be written before any specifier
```c
static [[nodiscard]]
u64 non_compliant_function( void )
{
   [...]
}


static [[nodiscard]] inline
u64 another_non_compliant_function( void )
{
   [...]
}


[[nodiscard]] static inline
u64 compliant_function( void )
{
   [...]
}
```

C-FUNC-XX - Function specifiers order shall be static, volatile and inline


C-LANG-XX - Language related rules
==

C-LANG-XX - Identifiers, files, strings and comments shall be written in english
