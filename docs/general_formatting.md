General formatting
===================

> [!CAUTION]
> Work-In-Progress.

Line length
------------

- Lines SHOULD NOT exceed **80** columns.
- Lines MUST NOT exceed **100** columns.

> [!NOTE]
> I like the **KISS** principle ( **K**eep **I**t **S**imple **S**tupid ).\
> Each line of code SHOULD only perform one operation at a time.\
> A line of code that exceeds 100 columns is often too complex and could be done on multiple lines.
>
> Having small lines also helps when having multiples files opened at the same time. Horizontal scrollbars are a nightmare, and the line-wrapping would make the code unreadable.\
> The argument could also be applied on code reviews, where the old version and the incoming one are often side-by-side.\If each line exceeds 100 characters, it makes the code less readable, and this is where bugs are not properly catched.
> 
> *If a programmer has difficulty to read the code, how can it understand what it does ?*

On VisualStudioCode, you can display vertical colored lines by using this code
in your `settings.json` file:

```json
   [...]
   "editor.rulers":
   [
      {
        "column": 80,
        "color": "#565656"
      },
      {
        "column": 100,
        "color": "#6e0000"
      },
   ],
   [...]
```

Function length
----------------

- Functions SHOULD NOT exceed 35 lines.

Avoid monolithic functions. Always apply the single-responsibility principle (SRP).
I saw too many functions bigger than 35 lines of code to make it a hard-limit.\
However, try to stick to this limit as much as you can. Often, your function becomes too large if:
- You have too many nested blocks
- Logic is duplicated and could be separated into smaller functions
- You can't easily deduce the purpose of the function.


Indentation
------------

- Spaces MUST be used for indentation. Tabs aren't allowed.
- An indentation MUST have a size of **3** spaces.

This is perhaps the most controversial opinion of the entire guide. I was a fervent user of tabs at the beginning.\
It was fine because I worked with people that were using the same indentation: A tabulation of size 4.

The day I started working with someone who had a different tab size (8, as recommended by the Linux kernel), the problems started.\
The code wasn't aligned correctly for me, and my code often exceeded the 80-column limit for him.

That's when I realised that it was important to see the same code in order to work together.\
And spaces guarantee that, because a space will always be the same size for everyone.

Being detached of the tabs, I wasn't limited to a 2, 4 or 8 indentation size.\
Thus, I experimented with different, from 2 to 6.
**3** was in my personal opinion the perfect size. Not too short, not too large.\
I like the way my code looks with a 3-size indentation, and thus this is the size I enforce\
in my guidelines.


Levels of indentation in a function
--------------

- A function MUST NOT exceed 3 levels of indentation.

Too many nested blocks of code makes the code less readable and hard to follow.\
- Use the Early Return pattern when you need to validate inputs, and if the subsequent logic
doesn't involve resources management.
- Nested blocks could be moved in a separate function (and could reduce code duplication)
- Reduce the work that the function is doing

```C
// DO
int function1( void )
{
   if ( [ ... ] )
   {
      return ERROR_1;
   }
   
   if ( [ ... ] )
   {
      return ERROR_2;
   }
   
   if ( [ ... ] )
   {
      return ERROR_3;
   }

   return OK;
}


// DON'T
int function2( void )
{
   if ( [ ... ] )
   {
      if ( [ ... ] )
      {
         if ( [ ... ] )
         {
            return OK;
         }
         else
         {
            return ERROR_3;
         }
      }
      else
      {
         return ERROR_2;
      }
   }
   else
   {
      return ERROR_1;
   }
}
```
