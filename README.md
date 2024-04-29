# C Coding Standards (WIP)

## IMPORTANT :
This document can be considered as an early Work-In-Progress draft.
Nothing is finished or polished yet.

#### Introduction

The main purpose of this repository is to set rules and guidelines that I'll follow on my personal projects.
Without an official document, I was tempted to make exceptions in my code, which wasn't consistent
with the rest of the project.
It's important to note that nothing is final. It could change depending of the needs, preferences and
experience.

**The C Coding Standards of this document are purely based on my personal preferences.**

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL
NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and
"OPTIONAL" in this document are to be interpreted as described in
RFC 2119.

## Summary
[Comments]( pages/comments.md )

## Formatting

- The maximum length of a line of code SHOULD be restricted to 80 when possible.
However, it MUST NOT be greater than 100.
Readability is important and it's a common practice to have multiple files opened at the same time. Having long lines will force users to either use the horizontal scroll bar to see the rest of the code, or wrap the code in the next line which isn't great for the readability.

- There is no maximum size for a particular function, but it's RECOMMENDED to have small functions with a specific task, rather than one big function that is doing the whole work.
Decoupling the code into small piece of logic also naturally reduces the code duplication.

- Open and closes braces are defining scopes inside our code, whether it's for the function scope, or an internal loop / piece of logic.
'{' and '}' MUST be places in a new line in order to keep a clear vision of the scope.
A scope SHOULD always be closed at the same column where it has been opened.

``` c
// Good
int function_name( void )
{
    // body of the function
    return 0;
}

// Bad
int function_name( void ) {
    // body of the function
    return 0;
}

// Bad
int function_name( void ) { return 0; }
```

### Constants
A constant is an immutable value and known as compile time.
It MUST be write in `UPPER_SNAKE_CASE`.

To define an integer constant, we MUST use the unnamed enum approach:
```c
enum
{
    CONSTANT_ONE = 0x40,
    CONSTANT_TWO = 12U,
    CONSTANT_THREE = [...]
};
```
The exceptions to this rule are for floating point values (like PII for example) and string based constants.
In this case, using the `const` approach is REQUIRED:

```c
double const MATH_PI     = 3.14159L;
double const MATH_RADIUS = 5.5L;
double const MATH_CALCUL = MATH_PI * MATH_PI * MATH_RADIUS;

char const *const MY_STRING = "Hello World!";
```
If `MATH_CALCUL` was a macro, we would have copied the whole calcul everywhere, which could be harmful on performance depending on the operation and the criticalness of the code.
It's also more error-prone to use a macro if we forgot the parenthesis. The result could differs depending on the operator precedence.

If your constants needs to be exposed in a header file, it is RECOMMENDED to add a prefix on your constants.
Knowing which header includes which constants will also be easier to follow if prefixes are consistents.

> [!TIP]
> - Don't use macro for constants.
> - Use an unname enum when possible, or use the `const` keyword.


### enums

An enum that regroups meaningful values together MUST be named.

```c
enum Direction // PascalCase
{ // Always on the next line
    Direction_NORTH, // Name of the enum as a prefix, separated with an underscore, and value name in UPPER_SNAKE_CASE.
    Direction_SOUTH, // You SHOULD Align the comments together to improve the readibility
    Direction_EAST,  // You MUST not typedef your enums.
    Direction_WEST,  

    // The number of elements in your enum. As it's a helper value, it shouldn't be used by the caller.
    // To separate it from the other enums values, the value name is in PascalCase instead.
    // The enum value _Count SHOULD only be defined if the enum values are starting from 0 and incrementing by one each time, without any jump.
    // Why ? Because having Direction_Count will incite the user to use the enum as an array-index.
    Direction_Count  // Having a comma for the last member of the enum is OPTIONAL.
}; // No typedef

enum FilePermission
{
    FilePermission_READ       = 1 << 0, // Could also be defined as 0b00000001
    FilePermission_WRITE      = 1 << 1, // Keep the same representation syntax for the entire enum.
    FilePermission_EXECUTE    = 1 << 2,

    // Separate by an empty line the bitflag declaration from the values created by composition of previously declared bitflags.
    FilePermission_READ_WRITE = FilePermission_READ | FilePermission_WRITE,
    FilePermission_ALL        = FilePermission_READ_WRITE | FilePermission_EXECUTE,

    // Masks are often useful to work with bitwise operations
    // If we need to define some masks alongside our enum to help in our implementation
    // We need to name them _Mask[...] in PascalCase.
    // Masks shouldn't be used by the caller. That's why we have defined FilePermission_ALL before instead of only _MaskAll.
    FilePermission_MaskNone = 0,
    FilePermission_MaskAll  = FilePermission_ALL

    // The Count enum value MUST NOT be defined when dealing with bitflag enums.
    // Otherwise, it will incite the user to use it as an index (from 0 -> Count).
    // FilePermission_Count
}

// It's also possible to define bitflags with the 0b syntax :
enum FilePermission
{
    FilePermission_READ    = 0b00000001,
    FilePermission_WRITE   = 0b00000010,
    FilePermission_EXECUTE = 0b00000100,

    [...]
}

// However, we can't separate our numbers with a digit separator like 0b0000'0001 in C until C23, which is not widely used for the moment.
// Dealing with 16 / 32 or even 64 bits could be really hard to read without separator, compared to 1 << 63 / 1 << 64.
```

## Struct
## Functions
## Comments
## Logic Flow ?
- early return, ...

## Naming

- snake_case for functions name
- camelCase for parameters and variables names
- PascalCase for enum, struct and unions
