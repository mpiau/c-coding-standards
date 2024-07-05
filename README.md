# C Language Coding Standards (CLCS)

> [!IMPORTANT]
> These coding standards are based on my own preferences and experiences.
> It's certainly not the best way to code in C (there's no particular standard above the others), but it's how I like to code in C.
>
> You can use it as you wish in your personal projects, or adapt it to your needs.
> The most important rule to follow in programming is to be **consistent** with the code around you.
> An important part of writing good code is following the style adopted and the guidelines of the project.
>
> Consistency in names, formatting, order and logic makes it easier for everyone to understand each other.
> It also helps us to focus on what the code is doing, so that bugs are not overlooked during reviews.

> [!CAUTION]
> This document is in **WIP** stage: Nothing is finished, everything is poorly written.
> At this stage, it's mostly a brain dump, but the fact that it's public motivates me to work on it.


## Getting started

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in RFC 2119.


## Summary

- [C Language Coding Standards (CLCS)](#c-language-coding-standards-clcs)
  - [Getting Started](#getting-started)
  - [C-FMT-XX - Formatting](#c-fmt-xx-c-formatting-rules)
    - [C-FMT-01 - Indentations](#c-fmt-01---indentations)
    - [C-FMT-02 - Lines width](#c-fmt-02---lines-width)
    - [C-FMT-03 - Files length](#c-fmt-03---files-length)
  - [TODO list](#not-exhaustive-todo-list)


## C-FMT-XX - Formatting rules

### C-FMT-01 - Indentations

- Spaces **must** be used for indentation. Tabs aren't allowed.
- Indentations **must** be **3** characters wide.

### C-FMT-02 - Lines width

- Each line **should** be limited to **79** characters.
- Each line **must** be limited to **99** characters.

### C-FMT-03 - Files length

- This is highly dependent of the context, but a C file (.h/.c) **should** not exceed **1000** lines of code to stay readable.


C-FUNC-XX - C Functions Rules
==

C-FUNC-XX - A function name shall be written in snake_case
--

C-FUNC-XX - A function shall have at most 4 parameters
--

C-FUNC-XX - A function with no parameter shall have a `void` parameter.
--

```c
void non_compliant_function();

void compliant_function( void );
```

C-FUNC-XX - A static function shall be only defined in a .c file.
--

C-FUNC-XX - Static functions shall only be used within the file they are defined.
--

C-FUNC-XX - Static functions shall be defined before non-static functions.
--

C-FUNC-XX - An unused function shall be either disabled by the preprocessor or deleted.
--

C-FUNC-XX - A non-static function definition shall have its associated declaration in a header file.
--

C-FUNC-XX - A non-void function shall have at least one return statement
--

C-FUNC-XX - A non-void function shall have a return statement at the end of the function
--

C-FUNC-XX - The return value of a function shall either be used or explicitly discarded
--

C-FUNC-XX - Function attributes and specifiers shall be written in a separated line
--
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
--
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
--

C-LANG-XX - Language related rules
==

C-LANG-XX - Identifiers, files, strings and comments shall be written in english
--


### Not exhaustive TODO List
----------
- [x] Write an introduction
- [ ] Write a summary
- [x] Write an indentation section
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
