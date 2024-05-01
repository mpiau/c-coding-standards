## Comments (WIP)

Comments are recommended, provided they are useful.
Don't explain HOW the code works: the code itself should be self-explanatory.
However, explain WHY you are doing something that isn't obvious.
It's important to document edge cases because a deeper context will be needed to
understand the code.
If you work with a ticket-software system like Jira, you could add the name of the ticket
in the comment to provide more details about the issue that is being fixed.


### Guidelines

- Comments MUST start with `// ` (`slash` + `slash` + `space`)
- A space MUST be added before a `// ` if the comment isn't at the beginning of a line.
- The usage of `/* ` and ` */` isn't allowed, even for multi-line comments.
- If you need to comment a block of code for local testing, you can use `#if 0` and `#endif` .
  Unlike `/* [...] */`, they support nesting.

```c
// This is a valid comment.

// This is a
// valid multi-line
// comment.

#if 0 // Commenting an entire function
int function( void )
{
   [...]
#if 0 // Nested block of code that was also commented
   [...]
#endif
   [...]
}
#endif
```

A comment, regardless of its form, increase the number of lines and the complexity of the code.
It can become more harmful than helpful to have useless comments where the code could have been
self-explanatory by carefully naming your functions / variables, and adopting naming conventions.

```c
#pragma once // Header file example

[...]

// Returns the name of the given country
char const *country_get_name( u64 countryId );
// The above comment is redondant and could have been deduced by the name of the function.

// If not found, an empty string will be returned.
char const *country_get_name( u64 countryId );
// Because the function could returns an invalid value, we are tempted to write it in a comment.
// While the intention is honorable, it could be avoided by changing how the function behave :

bool        country_get_name( u64 countryId, char const **outName );
char const *country_get_name_or( u64 countryId, char const *default );
bool        country_exists( u64 countryId );
// Here, no comments are needed to explain what the different functions will return.
// - country_get_name() emphasis on the potential invalidity of the data.
//   outName will be only usable if the function returns true.
// - country_get_name_or() allows the caller to customize the value returned by default.
// - country_exists() allows the caller to check the data validity beforehand.
```

> [!TIP]
> Always return a usable value at the end of your function.
> E.g. `NULL` is not considered as a usable value for a pointer.


### `TODO` comments

Sometimes, shortcuts and hacks must be made to fix a critical issue.
It's also possible that your current system is only partially implemented.

And while it's fine on a short-term perspective, these edge cases MUST be fixed on the long-term run.
Otherwise, it will join the rest of our technical debt.
**Creating technical debt is easy. Fixing it is exponentially harder over time**

Your `TODO` comment MUST follow the pattern below :
```c
// TODO @mpiau - <single line message>

// TODO @mpiau
//  <your message on multiple lines
//  with 2 spaces instead of 1 at the beginning>
```

> [!TIP]
> If immediate attention is required, you can also use `#warning <your message>` to give more
> visibility about the issue that needs to be fixed.


[← Introduction](../README.md) | [\<Next chapter\> →]()