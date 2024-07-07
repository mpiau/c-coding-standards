# The Unofficial C Language Coding Standards

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

In some examples, `[...]` is used to remove a chunk of code.


## Summary

- [The Unofficial C Language Coding Standards](#the-unofficial-c-language-coding-standards)
  - [Getting Started](#getting-started)
  - [C-FMT-XX - Formatting](#c-fmt-xx-c-formatting-rules)
    - [C-FMT-01 - Indentations](#c-fmt-01---indentations)
    - [C-FMT-02 - Lines width](#c-fmt-02---lines-width)
    - [C-FMT-03 - Files length](#c-fmt-03---files-length)
    - [C-FMT-04 - Comments](#c-fmt-04---comments)
    - [C-FMT-05 - Identifiers](#c-fmt-05---identifiers)
    - [C-FMT-06 - Structures](#c-fmt-06---structures)
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

### C-FMT-04 - Comments

- Single and multi-lines **must** use `//`
- The usage of `/*` `*/` for comments is not allowed.
- If you need to toggle a block of code, you **should** use `#if 0` and `#endif`
- At least one space **must** be written after `//`

```c
// A valid comment
//An ill-formatted comment

// =================== //
//  A header example  //
// =================== //

#if 0
// [code being disabled ...]
#endif // #if 0
```

> [!NOTE]
> The #if approach has several advantages over the use of `/* [...] */` :
> - It nests properly.
> - Toggling the code only require to change the `0` to `1`.
> - It removes the ability to write comments in the middle of a line of code, which for the most part breaks the reading of the line and makes it artificially more complex.

- Comments are recommended, provided they are useful.<br>
Don't explain HOW the code works: the code itself should be self-explanatory.<br>
However, explain WHY you are doing something that isn't obvious. It's important to document edge cases because a deeper context will be needed to understand the code.

> [!NOTE]
> A comment, regardless of its form, increase the number of lines and the complexity of the code.
> It can become more harmful than helpful to have useless comments where the code could have been self-explanatory by carefully naming your functions / variables and adopting naming conventions.

### C-FMT-05 - Identifiers

- Identifiers **must not** start with an underscore. It's reserved by the Standard.
- The length of an identifier **must not** exceed **31** characters.
- Identifiers **must** be written in english.
- Identifiers length **should** greater than **1**. Longer names are preferable if they improve the readability of the code, but there are some exceptions in mathematics code or loop variables.
- Avoid generic identifier names such as `tmp`. Taking the time to choose a coherent name for every identifier will greatly improve the readability of the code. Always think about future readers.

### C-FMT-06 - Structures

- `struct` identifiers **must** be written in PascalCase.
- `{` and `};` **must** be on their own line.
- Each line **must** only contain one variable declaration.
- Variable names and comments **can** be aligned according to your preferences.
However, keep it consistent between all definitions.
- The `struct` definition **must not** contain any `typedef`.
- A `struct` definition (comment included) **must** have at least one blank line at the beginning and the end of the definition.

```c
// Above code [...]

// Comment related to the structure defined below.
// It could be written on multiple lines, it's not important
struct Example
{
   int first;  // The first comment is aligned with the second one.
   int second; // Second comment
   unsigned int  third;  // Only the  last two variable names are aligned here
   unsigned long fourth; // to avoid an empty gaps with "first" and "second"
};

typedef struct Example Example;

struct SecondExample
{
   int           first; // This alignment could also be valid.
   unsigned int  second; // Just keep it consistent between all definitions.
};
```

```c
// Example of ill-formatted structs:
typedef struct IllFormattedTypedef
{
   [...]
} IllFormattedTypedef;

struct ill_formatted_case
{
   [...]
};

struct IllFormattedBraces {
   [...]
};

struct IllFormattedDeclaration
{
   int a, b;
};
struct IllFormattedBlankLines
{
   [...]
};
```

- Assigning / return an unnamed `struct` **must** comply with the following style:

```c
StructExample example = (StructExample) {
   .first  = [...]; // Like the struct definition, alignment is up to you as long as it stays consistent.
   .second = [...];
   .complexValue = (ComplexStruct) {
      [...];
   };
};

[...]

return (StructExample) {
   .first = [...];
   .second = [...];
   .complexValue = (ComplexStruct) {
      [...];
   };
};
```

### C-FMT-07 - Enums

### C-FMT-06 - Unions

### C-FMT-07 - Global variables

### C-FMT-08 - Static variables

### C-FMT-09 - Local variables


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
