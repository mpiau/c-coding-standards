# Enums

## Quick definition

An enum (or enumeration) in C is a user-defined data type representing a set of named integer constants.

### Formatting

```c
typedef enum CompassPoint CompassPoint;

enum CompassPoint : int
{
     CompassPoint_NORTH = 0
   , CompassPoint_EAST  = 1
   , CompassPoint_SOUTH
   , CompassPoint_WEST
};
```

### When to use

The best case scenario for the usage of enums is when you need to handle a specific set of constants that are related between each other.<br>

By using an enum, the scope to define these constants is clearly defined.<br>

As an example, let's say that we want to handle the signals that my program can receive at runtime. Reading `<signal.h>`, we can acknowledge that signals are macros and defined in multiple files (`<bits/signum-generic.h>` + `<bits/signum-arch.h>`)
```c
// From <bits/signum-generic.h>
[...]
#define	SIGINT   2	/* Interactive attention signal.  */
#define	SIGILL   4	/* Illegal instruction.  */
#define	SIGABRT  6	/* Abnormal termination.  */
#define	SIGFPE   8	/* Erroneous arithmetic operation.  */
#define	SIGSEGV 11	/* Invalid access to storage.  */
#define	SIGTERM 15	/* Termination request.  */
[...]

// From <bits/signum-arch.h>
[...]
#define SIGURG   23	/* Urgent data is available at a socket.  */
#define SIGSTOP  19	/* Stop, unblockable.  */
#define SIGTSTP  20	/* Keyboard stop.  */
#define SIGCONT  18	/* Continue.  */
[...]
```

Reading the content of these headers, several questions can be raised:
- Do we have more signals defined somewhere else ?
- Do we need to include another header ?
- Does every macro starting with SIG a signal ?
- [...] ?

At the end, we will need to read the documentation to retrieve the complete list of signals and their associate SIG[...] macro.

Packing these constants into a single enum makes it more readable:
```c
enum Signal
{
     Signal_SIGINT  =  2  /* Interactive attention signal. */
   , Signal_SIGILL  =  4  /* Illegal instruction. */
   , Signal_SIGABRT =  6  /* Abnormal termination. */
   , Signal_SIGFPE  =  8  /* Erroneous arithmetic operation. */
   , Signal_SIGSEGV = 11  /* Invalid access to storage. */
   , Signal_SIGTERM = 15  /* Termination request. */
   , Signal_SIGCONT = 18  /* Continue. */
   , Signal_SIGSTOP = 19  /* Stop, unblockable. */
   , Signal_SIGTSTP = 20  /* Keyboard stop. */
   , Signal_SIGURG  = 23  /* Urgent data is available at a socket. */
}
```
As a bonus point, we are also reducing the number of macros and the risk of redefining them.

### Why an enum ?

- An enum provide symbols for the debugger, which can help debugging the program.
- An enum can be used in a switch statement.
- An enum can be used to initialize static variables and array size.
- An enum don't have side-effect(s) that a define could potentially produce

> [!NOTE]
> Not exhaustive list, to complete.
