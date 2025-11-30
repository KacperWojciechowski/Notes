# C Coding Standard
> Author: Kacper Wojciechowski

## Code architecture
#### Modularity


#### Access to data and functions
1. **Private** - entities within code (functions, variables, consts, macros, etc.) that are not meant to be available by everyone, and are meant to be hidden from the outside perspective. Those entities will be exclusively placed in the source files that use them, shall not have any of their signatures exposed in any header files and will be marked using `static` keyword to prevent visibility leaks due to possible `extern` definitions. This scope should be used by default, especially including things like internal state of given module.
> __NOTE__: This pattern aims at ensuring the safety and validity of the private data, and follows a paradigm typically used in Object Oriented Programming, where limiting the visibility of the data protects it from accidental or intentional corruption.

2. **Public** - entities within code that are meant to be accessible by other entities (eg. interface of a module). These entities will require to be visible in the corresponding headers.
> __IMPORTANT__: Some modules may require the ability to have their internal state affected by outside things (eg. setting an error/status flag in an internal register, registering an outside container that will be accessed by the module, etc.). However such entities should not be exposed directly, and instead the module should their own API for affecting this state, so that the module has complete control over how its internal state is managed, to ensure **it is valid at all times**.

## Functions
#### Declarations and definitions
1. The place where you want to put function prototypes, depend highly whether the function is intended to be public or not and will follow the rules described in the [Access](#access) section.
2. Header files should **not** contain function definitions - only declarations. If a function is the be *inlined*, the header will contain only it's prototype with the `inline` keyword (or `always_inline` attribute).
  
#### Parameters
1. The **first thing** a function needs to do is to **ensure all parameters passed to it are valid for its logic** (eg. pointers are not null and point to a valid value, numeric parameters are within expected range, etc.). This should be done either with **asserts** or **early returns** depending on the function's logic.
2. If any of the function parameters has an invalid value according to the function's logic, then depending on the logic the function implements, it will either **early return** a default value, or fail at an `assert_param` if the function is never supposed to be called with the invalid value. Using `assert_param` is highly recommended for both security and optimization purposes: 
  2.1. **Unit tests** that are run in `Debug` profile will be able to capture the invokation of assert handler, so it drastically increases the **chance of catching whenever something goes wrong** in any of the execution branches.
  2.1. Asserts are typically **disabled** in `Release` profile at the preprocessor level, so it **removes the checks made in runtime**.
3. If there is some processing required in order to check the validity of a parameter, the function will do only as little processing as possible to make sure all parameters are valid, before it proceeds to its logic.
4. If a function can perform it's logic regardless the value or validity of one or more parameters (**excluding** return parameters), it is a sign that either the parameter is redundant, or the function has more than one responsibility and needs to be split.
5. `Bool` parameters (**excluding** things like register flags) are a sign that a function tries to combine several responsibilities into one. As such, the function should be split into separate functions, and it should be the decision of the upper-level function which calculates the `bool` parameter, which one of those separate functions to invoke. In case where the `bool` parameter in question introduced only partial difference in the function logic and the rest of the logic is shared, the function should be split into one function for the shared logic, and one function per the `bool` branch.
6. `NULL` value can be a valid value, depending on the function's logic. A typical case for this would be an auxiliary return parameter, that might not interest the caller, and which does not disturb the function's logic if absent. Accepting the `NULL` as a valid value in such case allows the simplification of some function calls.
7. When passing a pointer to a buffer, the function must also take a parameter that indicates the size of the buffer, to allow for bounds checks when accessing the memory.

#### Function body
1. Try to keep the function bodies and logic as simple as possible.
2. Limit the length of a function to the extent where they are easily comprehensible. The perfect rule of thumb is that a function body should fit entirely on your screen, which typically translates to roughly **60 lines of code** in standard IDEs. If a function body is larger than that, seriously consider delegating part of its logic to separate, smaller functions.
> __NOTE__: If the delegated logic is not to be seen outside, use the **private** function approach described in [Access to data and functions](#access-to-data-and-functions) section.
> __IMPORTANT__: Avoid using macros for visually separating the logic. Macros have a nasty habit of inflating very quickly and can be difficult to analyze, especially when they become either complex expressions, or their expressions are nested more than 2 levels.
1. When making functions that carry out some procedure, divide the procedure into phases and make the function body reflect that split into sections, by either separating the code into visibly separate blocks, or directly carry the section out into a separate function.
2. When your function performs processing that depends on several conditions, prioritize checking the conditions first, doing only the bare minimum of processing. This allows for better error handling and makes using the "early return" pattern significantly easier.
3. Avoid nesting control structures and conditional statements. Instead of this, prefer to invert the conditions and separate them, so they can be checked in an "early return" manner (either using the return or `goto` to handle situations where a condition is not fulfilled). This makes the code easier to analyze and reduces the cyclomatic complexity.
> __NOTE__: A maximum level of nesting that is fine, is two levels, which is having a single level of control structure (`if`/loop) inside an outer control structure (eg. a nested `for`, or `if` checks within a `for`/`if`). Having any more nesting than this prompts the need to evaluate how it can be redesigned to have the complexity simplified (some options are inverting and splitting conditions or extracting the inner control structure into a separate function). The goal is not that the program cannot execute multiple nested control structures - it is to keep the nesting within each function simple for analysis.

#### Use of goto

## Data entities
#### Declaration, definition and initialization
1. When you create a variable, array, pointer or a structure, it **always** has to be initialized right away, either with it's target value, or some default value that is considered **valid** for given circumstances. 
> __NOTE__: Values that are considered **invalid for processing** but thus allow the function to **detect if something is wrong**, will also be considered a **valid default** value.
2. When initializing a pointer, use `NULL` **instead** of `0` or `{0}` as default value, to avoid confusion and make it much more verbose that the pointer is not fit for dereference.
3. When initializing a structure, use the **designated member** notation (`MyStruct_t myStruct = {.field1 = val, .field2 = val}`) so the member values are **explicitly described** in the syntax (thus not considered "magic values").
4. When working with pointers, do not use more than 2 layers of indirection, to avoid complicated chains and multiple dereferences.
5. Keep the structure nesting flat, not deeper than 2 layers (the outer struct containing a flat inner struct).

#### Assignments and expressions
1. If you perform operations during assignment (eg. calculating things), wrap the expression in `( )` for better visibility and protection from operator precedence bugs.
2. In compount expressions (eg. a conditional where one or both sides consist of some calculation, or a conditional that consists of several conditions compounded by logic operators), each of those expressions needs to be wrapped in `( )` for better readability and to protect yourself from the operator precedence bugs.
3. Use definitions from the `<stdbool.h>` standard library header for logic types and literals instead of the `int` with `0` and `1` values, to explicitly show that given variable / expression is to be considered a logical expression, instead of a calculation.

#### Safe data access
1. When working with dynamic allocation, you must always validate whether the allocation was successful right after the allocation, **before you perform any other operations**.
2. Before dereferencing a pointer, you need to always ensure the pointer has a non-`NULL` value (as long as the pointer value does not change, checking once is sufficient for multiple dereferences). 
> __NOTE__: An exception to this rule is when the pointer is assigned the address of other entity directly in the body of the same function that dereferences it (an example would be an iterator for traveling over an array).
> __IMPORTANT__: The exception mentioned above applies only within the local scope of the exact same function - if this is done by other function that called your function providing the pointer, your function must still validate the pointer before dereferencing it.
3. When iterating over a buffer - either an automatically or dynamically allocated one - it should only be done using the `for` loop which specifies the initial iterator value, and despite any other conditions, is guarded by checking whether the iterator does not violate the upper bounds.

#### Lifetime control and memory management
1. Prefer local scope over global scope. Try to limit the lifetime of the variables/structures to as narrow scope as possible. This serves both optimizing RAM usage, aswell as mitigating an entire class of vulnerabilities standing from unintended variable modification/access and leaking data visibility.
2. Prefer automatic data (variables, structures, arrays) instead of dynamically allocated data. This serves not only increasing performance, but most importantly having a significantly better control over lifetime of objects and reducing the memory leaks.
3. Prefer allocating a complete chunk of memory you might require right away, instead of iteratively allocating small blocks. This makes such allocations much easier to analyze - both statically and at runtime, ensuring no boundary violations of the allocated block and much easier lifetime and freeing of the memory, thus reducing memory leaks.

## Header files
1. When including a header file, use path notation from some top-level include folder, instead of the header file name alone, to make it easier to see what module the header file belongs to.
> __NOTE__: This sadly cannot be applied to includes in test files due to the limitations of the `Ceedling` and `CMock` frameworks, as it interferes with the frameworks resolving the source files that correspond to the headers.

## Macros
1. Macros' values and parameters used in the expressions the macro expands to, always need to be sorrounded by `( )`, to avoid bugs standing from the evaluation order when the preprocessor expands the macro (namely bugs related to operator precedence).
2. Never put semicolon (`;`) at the end of the value of a macro definition. If a macro serves as a way to name some operation (eg. bitwise operations on registers) emulating an inlined function, place the semicolon at the place of calling the macro, as you would with a function call, and not within the macro expression itself. This allows for potentially using the macro in other expressions (eg. as a condition for an `if` statement) without breaking the syntax.
3. Simple expressions that are hard to read from the language's syntax alone (bitwise operations are a notorious offender here) are a good candidate to be aliased using simple macros.
4. If you want to alias conditions using macros, make one macro per condition.
> __NOTE__: In case of composite conditions, it is acceptable to have each of the conditions aliased as a macro, and then have one macro alias the composing of the conditions, as long as the overall depth of the macro expansions is not bigger than 2 levels.

## Loops
1. All loops need to have a fixed uppder bound of iterations that can be proven using static analysis, unless the loop is meant to run indefinitely (`while(true)`).
2. Use `continue` and `break` in loops where applicable, to simplify the loop body
3. `goto` is allowed in loops, but only for moving within a given scope or outside of said scope (**not** inside a scope), and **only in forward direction**. Typical application for `goto` in loops is to exit a nested loop entirely (moving outside of the scope in which the goto is called, in a forward direction).
> __IMPORTANT__: "forward direction" in this case means that the `goto` should not be used for going back to some previous operation, and should only serve to skip a portion of the operations that are further down the line.
> __IMPORTANT__: "within a given scope or outside of said scope" means that the `goto` can be used to skip several operations inside the same scope (that can include skipping over entering a narrower scope), or to escape the scope to a higher one. `goto` should **not** be used to enter a narrower scope from the outside, as it easily interferes with things such as automatic memory allocation and can lead to an undefined behavior or straight up crash of the program.


## Hertz-specific aspects
#### Codebase structure
1. Header guards should be named after the full path to accessing the header from the project's root directory. This serves avoiding define collisions between two files that have the same name but are placed in different directories.


// Legacy ----------------------------------------------------------------------------

## Headers
- what symbols should be present in the header

## Source files
- switch cases need to end up either with `break` or `return` if they are not fall-through, even at the end of the switch block
- if a case is fall-through, it will be marked as such using a comment
- all loops need to have a fixed upper bound of iterations that can be proven using static analysis, unless the loop is meant to run indefinitely (`while(true)`)
- when dealing with dynamic allocation of data shared between functions, the dynamically allocated data must be seen as dynamically allocated only within the logical entity that allocated it - all other entities must have no idea how or when the data is allocated
- if your logical entity operates on dynamically allocated data, it alone is responsible for handling it's memory (it must be the one that allocates it and the one that frees it)
- you can call a function only when you make sure that all arguments you pass to it are considered valid by that function
- if you operate with conditional compilation of logic (eg. part of a function executes only if given compilation flag is set), instead of removing that piece of code via preprocessor definitions, wrap it in `if` statement that is dependend on a macro that's defined to either `true` when the compilation flag is set, or `false` when it is not present. This allows for statically analyzing and automated testing of all possible paths for the code **including** parts that depend on conditional compilation
- in situations where you assign some value based on condition, use ternary operator instead of `if/else` blocks
- unless each enum value has a non-subsequent value (eg. `one-hot encoding`), specify only the value of the first element - compiler will calculate the values of subsequent elements as increasing by `1` automatically
- if return value of a function varies:
    - if there has to be processing done before you can return, make a return variable at the start of the bfunction body with default value and modify it between processing as needed
    - if you can return right away, return
    - if it's based on conditional and there is no more processing to do after calculating the condition, use `return (condition);` syntax
- when returning a value (be it variable or a struct) you must make sure the returned value is valid in accordance to the logic of the function and data that it returns (eg. if a function searches for element and does not find the element, it needs to return a default element that has valid and consistent value, eg. counters cannot be negative or violate the relationship between them)
- if some value is not used, mark it using `(void)` or a compiler attribute
- if a switch statement handles all enum values, do not place the `default` case - this allows to catch situations when a new value is unhandled at the compile time
- if declarations in headers do not require knowing the size of a structure (eg. you declare a function that takes pointer to some structure), use forward declaration instead of including the structure definition and include the definition in the source file instead. This helps with drastically limiting the dependency graph, and decreases the chances of include cycles.
- headers should have as little includes inside as possible
- in order to fix an include cycle or if you expect that an include cycle may occur, extract the declarations that need to be shared into a separate header, and make both of the colliding headers include that common header instead
- limit the includes only to the things that you actually use, remove any redundant includes
- do not prematurely declare data - declare variables only right before you use them and only inside the scope you use them in. This gives you drastically more control over their lifetime, optimizing the resource usage and protecting against a whole class of errors
- if a variable or struct is not to be modified, it needs to be defined as `const`
- if a parameter serves a read-only purpose, it needs to be `const` (pointers included)
- if converting between signedness, you need to make sure the conversion will be valid (no data corruption due to re-purposing the MSB to sign enconding and no validation of the target type boundaries)
- avoid returning through pointer as much as possible
> An exception is a pattern where a high-level entity provides you with something like a register to raise flags or store data, that this high-level entity will process on its own in a centralized manner
- prefer `sizeof()` operator over hard-coded sizes
- if accessing some data is complicated or an operation is not readable (eg. bitwise operations, pointer arithmetics), alias them using a macro
- if a numeric literal is to be treated as without a sign, mark it using the `u` specifier
- when formatting numeric values (especially floating point values), specify the number of characters available for them in the format string. This allows for statically calculating the resulting string size to ensure it will not violate the bounds of the buffer it's written into
- use the `n-`variants of the string manipulation stdlib functions instead of the regular ones (eg. `snprintf` instead of `sprintf`). They safeguard from overflowing the buffer it writes into.
- if you want to leave information about what needs to be done in the code in the future, make a comment and start it with capital `TODO` word, so it can be easily found using tools like `grep`
- do not use magic numbers - unless the context strictly explains what the value means (eg. `setFailureCounterValue(0)` or `SomeStruct myStruct = {.failureCounter = 0}`), alias the value or store it in a variable which name explains its meaning
- avoid returning `void*`, unless the function returns a parameter that was also provided via `void*` (storing the function return to `void*` is ok).
- avoid `void*` parameters, because you cannot consistently check them neither via static analysis nor via runtime unit testing - they open a huge window to memory-corruption-related vulnerabilities and can be considered "downcasting".
- if your function requires a bool parameter which changes how it processes things inside, it should be split into two separate functions eliminating the `bool` parameter. Passing the bool value transparently or routing the processing to different functions based on the `bool` parameter is dubious but acceptable.
- do not return local-scope dynamically allocated data. Dynamically allocated data needs to be cleared in the same scope it was allocated in (excluding things like static global state of some logic entity, as this data is considered of global state but is allocated inside some initialization function)
- the structure of the source file should be as follows:
    - includes
    - defines and global data
    - private static functions prototypes
    - public functions
    - private static functions definitions
    This makes it so if someone else is trying to use your code, he has all the relevant information at the top, and the functions that you don't want to expose are tucked at the bottom
- error handling needs to be constructed in a way, that guarantees that the program does not crash or HardFault (intentional system restart to return to a valid state is acceptable). The code must implement a no-crash policy and have recovery mechanisms.
- always check the return values of the functions, unless you intentionally do not care about them - then mark this via `(void)` or compiler attribute in the function call
- all possible code paths need to be handled - you cannot have unhandled errors
- external dependencies (eg. libraries) should be added to the project using the `git submodule` functionality and cloned into a designated folder in the project's root directory. The includes of all the external dependency headers should be a path to the header from the said top-level directory.
- if a function obtains external input (eg. from an interface, from a network), unless said function is an ISR, it needs to validate the input and make sure it does not contain corrupted or malicious data.
- projects should be configured to be automatically stamped with the git commit hash during the compilation process. This gives a huge insight when debugging a binary that has already been deployed.
- in case of very long switch statements, a Look-Up Table should be considered as an alternative, unless the incured memory/performance penalty is too big
- if you need a dynamic structure, prefer ring buffer and memory pool over dynamic allocation. Those structures typically wrap automatic memory placed on stack, so they can be easily statically analysed and give very easy bounds checking.
- extern clauses can only be used at global scope
- 

## Rules for using goto
- goto can be used, but only for specific applications, and only within the local scope of a function (a.k.a. you cannot use goto to go outside the body of the function which calls it)
- use goto only to move within the same scope, or to a wider scope
- never use goto to move inside a narrower scope from the outside
- two primary use cases for goto is exiting a nested loop (jumping out of the nesting entirely, but only forward in the function body) and jumping to a post-processing section placed at the end of the function (mimicking `try/catch/finally` blocks)

## Comments
- avoid unnecessary comments
- comments should explain additional context or reasons for specific implementation decision, not **how** something is done - this should be readable in the code
- For multiline comments prefer C block comment instead of multiple one-line comments

## Code structure
- divide code into single-responsibility abstract entities
- expose only the interface on the entity, do not expose any internal operations or data
- prefer passing via pointer over global access

## Naming
- names should be made in a way, that allows to roughly tell what given function does after reading the name alone
- do not shorten names, except for using standard / commonly known acronyms
- mixing Camel Case and Snake Case is allowed
- make macro names only using underscores (`_`) and only capitalized letters