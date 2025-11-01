# === C++ Roadmap

## --- Overview

This roadmap was crafted with the intent to craft a comprehensive path for learning C++ language in the most user-friendly manner. As such, the main component of this roadmap is the ***core path*** marked with the *green* color, that leads the reader through all the necessary, fundamental features of the language while limiting the amount of concepts and caveats to grasp.

As for the fact that many of the functionalities moved off of the *core path* are widely utilized and really helpful in most of the more advanced projects, they had been grouped into subjects that could be evaluated in terms of difficulty, and branch off of their related *core path* topic.

## --- Intended approach for the reader

In order to make the best out of this roadmap. it is recommended to:

1. First go through the entire ***core path*** of the roadmap, marked with the *green* color;
2. Introduce topics marked by the *khaki* color;
3. Introduce topics marked by the *orange* color;
4. Introduce topics marked by the *red* color;

The increase in difficulty as per the above list inversely correlates with the frequency at which those features are used in typical projects. This suggests that going up the difficulty chain gradually also promises the biggest skill increase with the least investment.

As real-life software projects vary vastly depending on their application, it must be stated that the priority of features for each and every reader might be different, and you may need to jump around the difficulty chain as need be.

## --- Roadmap

```plantuml
@startuml

legend top left
|= Color |= Difficulty |
|<back:#MediumSeaGreen>            </back>| Core Path |
|<back:#Khaki>            </back>| Intermediate |
|<back:#Orange>            </back>| Advanced |
|<back:#IndianRed>            </back>| Very Advanced |
end legend
/' ------------------------------ Lessons declaration ------------------------------ '/

state "1. Basic program" as Lesson_1 #MediumSeaGreen
state "2. Variables" as Lesson_2 #MediumSeaGreen
state "2.1. In-depth primitive\ndata types (*)" as Lesson_2_1 #Khaki
state "2.2. Type\nconversion (*)" as Lesson_2_2 #Khaki
state "2.3. Literals (*)" as Lesson_2_3 #Khaki
state "2.3.1. Escape characters (*)" as Lesson_2_3_1 #Khaki
state "2.3.2. Type deduction (*)" as Lesson_2_3_2 #Orange
state "2.4. Strings" as Lesson_2_4 #MediumSeaGreen
state "2.5. Advanced\noutput (*)" as Lesson_2_5 #Khaki
state "2.4.1. String\nsearching (*)" as Lesson_2_4_1 #Orange
state "2.4.2. String\nmodification (*)" as Lesson_2_4_2 #Khaki
state "3. Basic math" as Lesson_3 #MediumSeaGreen
state "2.6. Compile-time\nevaluation (*)" as Lesson_2_6 #Orange


state "3.1. Advanced\nfloating-point (*)" as Lesson_3_1 #IndianRed
state "4. Conditionals" as Lesson_4 #MediumSeaGreen
state "4.1. Implicit bool\nconversions (*)" as Lesson_4_1 #Khaki
state "5. Iterations" as Lesson_5 #MediumSeaGreen
state "4.2. Compile-time\nconditionals (*)" as Lesson_4_2 #IndianRed


state "6. Static arrays" as Lesson_6 #MediumSeaGreen
state "6.1. Advanced\nstatic arrays (*)" as Lesson_6_1 #Khaki

state "7. Functions" as Lesson_7 #MediumSeaGreen
state "7.1. Advanced functions (*)" as Lesson_7_1 #Orange
state "7.2. Scopes" as Lesson_7_2 #MediumSeaGreen
state "7.3. Side effects (*)" as Lesson_7_3 #IndianRed

state "8. Splitting code into files" as Lesson_8 #MediumSeaGreen
state "8.1. In-depth codebase\nstructure (*)" as Lesson_8_1 #Khaki
state "8.1.1. External\nlibraries (*)" as Lesson_8_1_1 #IndianRed
state "8.1.2. Linking errors (*)" as Lesson_8_1_2 #Orange
state "8.2. Macros (*)" as Lesson_8_2 #Orange

state "10. File operations" as Lesson_10 #MediumSeaGreen
state "10.1. Advanced file operations (*)" as Lesson_10_1 #Orange
state "11.3. Structure\nmemory concerns (*)" as Lesson_11_3 #Orange

state "11.2. Structure data\naccess (*)" as Lesson_11_2 #Khaki
state "11. Structures" as Lesson_11 #MediumSeaGreen
state "9. Enumeration types" as Lesson_9 #MediumSeaGreen
state "9.1. In-depth enums (*)" as Lesson_9_1 #Khaki

state "12. Namespaces" as Lesson_12 #MediumSeaGreen
state "11.1. Default values (*)" as Lesson_11_1 #Khaki
state "11.4. In-depth look\ninto structures (*)" as Lesson_11_4 #Khaki
state "12.1. Anonymous\nnamespaces (*)" as Lesson_12_1 #Khaki
state "13. Access to original data" as Lesson_13 #MediumSeaGreen


state "13.1. Conversions\nof pointers (*)" as Lesson_13_1 #Orange
state "14. Dynamic allocation" as Lesson_14 #MediumSeaGreen
state "13.2. Advanced pointers (*)" as Lesson_13_2 #Khaki

state "14.1. Memory model (*)" as Lesson_14_1 #Orange
state "14.2. Iterators (*)" as Lesson_14_2 #Khaki
state "14.3. Advanced memory\nmanagement (*)" as Lesson_14_3 #IndianRed
state "8.1.3. Managing compiler\noptimizations (*)" as Lesson_8_1_3 #IndianRed
state "8.1.4. Integration\nwith C code (*)" as Lesson_8_1_4 #IndianRed
state "8.3. Modules (*)" as Lesson_8_3 #IndianRed
state "11.5. Unions (*)" as Lesson_11_5 #Orange
state "15.1. Leveraging compiler\nmethod generation (*)" as Lesson_15_1 #Orange
state "15. Object Oriented\nProgramming Basics" as Lesson_15 #MediumSeaGreen
state "14.4. Optional values (*)" as Lesson_14_4 #Khaki
state "16. OOP Data Management\nConcepts" as Lesson_16 #MediumSeaGreen
state "15.2. Class performance optimization (*)" as Lesson_15_2 #Orange

state "17. Advanced access\nof class contents" as Lesson_17 #MediumSeaGreen
state "17.1. Making class compliant\nwith advanced language\nfeatures (*)" as Lesson_17_1 #IndianRed
state "17.2. Memory access to class content (*)" as Lesson_17_2 #IndianRed

state "18. Const-suitable classes" as Lesson_18 #MediumSeaGreen
state "18.1. Advanced object\nconstruction (*)" as Lesson_18_1 #Orange
state "18.2. Advanced const object\nproperties (*)" as Lesson_18_2 #IndianRed
state "19.1. Multiple inheritance (*)" as Lesson_19_1 #Orange
state "19. Inheritance" as Lesson_19 #MediumSeaGreen
state "20. Polymorphism" as Lesson_20 #MediumSeaGreen

state "21.1. Advanced\nerror handling (*)" as Lesson_21_1 #Orange
state "20.1. Advanced\npolymorphism\nconcepts (*)" as Lesson_20_1 #IndianRed
state "20.2. Advanced operator\noverloading (*)" as Lesson_20_2 #IndianRed
state "20.3. Improving\nreadability (*)" as Lesson_20_3 #Khaki
state "21. Error handling" as Lesson_21 #MediumSeaGreen
state "20.4. Design Patterns" as Lesson_20_4 #MediumSeaGreen

state "22. Templates" as Lesson_22 #MediumSeaGreen
state "22.1. Advanced template\nconcepts (*)" as Lesson_22_1 #Orange
state "22.2. Adaptive templates (*)" as Lesson_22_2 #IndianRed
state "22.3. Templates vs codebase (*)" as Lesson_22_3 #IndianRed

state "23. STL - Standard Template Library" as Lesson_23 #MediumSeaGreen
state "23.1. Useful\nstandard libraries (*)" as Lesson_23_1 #Khaki
state "23.2. Popular\nthird-party libraries (*)" as Lesson_23_2 #Orange
state "24. Lambdas and\nHigher Order Functions" as Lesson_24 #MediumSeaGreen
state "24.1. Storing functions (*)" as Lesson_24_1 #Khaki
state "24.2. Transforming data (*)" as Lesson_24_2 #Orange

state "25. Concurrency" as Lesson_25 #MediumSeaGreen
state "25.1. In-depth concurrency" as Lesson_25_1 #MediumSeaGreen
state "25.2. Asynchronous programming" as Lesson_25_2 #MediumSeaGreen
state "26. Sharing resources\nbetween threads" as Lesson_26 #MediumSeaGreen
state "26.1. Synchronized types (*)" as Lesson_26_1 #Orange

state "27. Resolving problems\nwith concurrency" as Lesson_27 #MediumSeaGreen
state "27.1. Interacting with the OS" as Lesson_27_1 #IndianRed

/' ------------------------------ State connections ------------------------------'/

[*] -down-> Lesson_1
Lesson_1 -down-> Lesson_2

Lesson_2 -down-> Lesson_3
Lesson_2 -up[dashed]-> Lesson_2_1
Lesson_2 -up[dashed]-> Lesson_2_2
Lesson_2 -down[dashed]-> Lesson_2_3
Lesson_2 -right[dashed]-> Lesson_2_4
Lesson_2 -up[dashed]-> Lesson_2_5
Lesson_2 -down[dashed]-> Lesson_2_6
Lesson_2_3 -down[dashed]-> Lesson_2_3_1
Lesson_2_3 -up[dashed]-> Lesson_2_3_2
Lesson_2_4 -up[dashed]-> Lesson_2_4_1
Lesson_2_4 -down[dashed]-> Lesson_2_4_2

Lesson_3 -down-> Lesson_4
Lesson_3 -down[dashed]-> Lesson_3_1

Lesson_4 -down-> Lesson_5
Lesson_4 -down[dashed]-> Lesson_4_1
Lesson_4 -down[dashed]-> Lesson_4_2

Lesson_5 -down-> Lesson_6

Lesson_6 -down-> Lesson_7
Lesson_6 -right[dashed]-> Lesson_6_1

Lesson_7 -down-> Lesson_8
Lesson_7 -left[dashed]-> Lesson_7_1
Lesson_7 -up-> Lesson_7_2
Lesson_7 -right[dashed]-> Lesson_7_3

Lesson_8 -down-> Lesson_9
Lesson_8 -right[dashed]-> Lesson_8_1
Lesson_8 -left[dashed]->Lesson_8_2
Lesson_8 -left[dashed]->Lesson_8_3
Lesson_8_1 -down[dashed]-> Lesson_8_1_1
Lesson_8_1 -up[dashed]-> Lesson_8_1_2
Lesson_8_1 -down[dashed]-> Lesson_8_1_3
Lesson_8_1 -right[dashed]-> Lesson_8_1_4

Lesson_9 -down-> Lesson_10
Lesson_9 -left[dashed]-> Lesson_9_1

Lesson_10 -down-> Lesson_11
Lesson_10 -right[dashed]-> Lesson_10_1

Lesson_11 -down-> Lesson_12
Lesson_11 -down[dashed]-> Lesson_11_1
Lesson_11 -down[dashed]-> Lesson_11_2
Lesson_11 -left[dashed]-> Lesson_11_3
Lesson_11 -right[dashed]-> Lesson_11_4
Lesson_11 -right[dashed]-> Lesson_11_5

Lesson_12 -down-> Lesson_13
Lesson_12 -left[dashed]-> Lesson_12_1

Lesson_13 -down->Lesson_14
Lesson_13 -left[dashed]->Lesson_13_1
Lesson_13 -right[dashed]->Lesson_13_2

Lesson_14 -down-> Lesson_15
Lesson_14 -down[dashed]-> Lesson_14_1
Lesson_14 -left[dashed]-> Lesson_14_2
Lesson_14 -right[dashed]-> Lesson_14_3
Lesson_14 -down[dashed]-> Lesson_14_4

Lesson_15 -down-> Lesson_16
Lesson_15 -down[dashed]-> Lesson_15_1
Lesson_15 -down[dashed]-> Lesson_15_2

Lesson_16 -down-> Lesson_17

Lesson_17 -down-> Lesson_18
Lesson_17 -right[dashed]-> Lesson_17_1
Lesson_17 -left[dashed]-> Lesson_17_2

Lesson_18 -down-> Lesson_19
Lesson_18 -left[dashed]-> Lesson_18_1
Lesson_18 -right[dashed]-> Lesson_18_2

Lesson_19 -down-> Lesson_20
Lesson_19 -left[dashed]-> Lesson_19_1

Lesson_20 -down-> Lesson_21
Lesson_20 -right[dashed]-> Lesson_20_1
Lesson_20 -left[dashed]-> Lesson_20_2
Lesson_20 -right[dashed]-> Lesson_20_3
Lesson_20 -down-> Lesson_20_4

Lesson_21 -down-> Lesson_22
Lesson_21 -right[dashed]-> Lesson_21_1

Lesson_22 -down->Lesson_23
Lesson_22 -right[dashed]-> Lesson_22_1
Lesson_22 -left[dashed]-> Lesson_22_2
Lesson_22 -up[dashed]-> Lesson_22_3

Lesson_23 -down-> Lesson_24
Lesson_23 -right[dashed]-> Lesson_23_1
Lesson_23 -left[dashed]-> Lesson_23_2

Lesson_24 -down-> Lesson_25
Lesson_24 -left[dashed]-> Lesson_24_1
Lesson_24 -right[dashed]-> Lesson_24_2

Lesson_25 -down-> Lesson_26
Lesson_25 -left-> Lesson_25_1
Lesson_25 -right-> Lesson_25_2

Lesson_26 -down-> Lesson_27
Lesson_26 -right[dashed]->Lesson_26_1

Lesson_27 -left[dashed]-> Lesson_27_1

/' ------------------------------ Content of the lessons ------------------------------'/

/' ========== Basic program ========== '/
Lesson_1 : - program structure
Lesson_1 : - output operation
Lesson_1 : - #include <iostream>

/' ========== Variables ========== '/
Lesson_2 : - primitive types
Lesson_2 : - variables
Lesson_2 : - input operation
Lesson_2 : - declaration
Lesson_2 : - initialization
Lesson_2 : - const

/' ========== In-depth primitive data types ========== '/
Lesson_2_1 : - signedness
Lesson_2_1 : - integer types of different size
Lesson_2_1 : - ASCII
Lesson_2_1 : - char arithmetic
Lesson_2_1 : - capitalizing char using math
Lesson_2_1 : - std::toupper()
Lesson_2_1 : - std::tolower()

/' ========== Type conversion ========== '/
Lesson_2_2 : - concept of casting
Lesson_2_2 : - C-style cast
Lesson_2_2 : - static_cast
Lesson_2_2 : - const_cast

/' ========== Literals ========== '/
Lesson_2_3 : - char literals
Lesson_2_3 : - string literals
Lesson_2_3 : - int literals
Lesson_2_3 : - float literals
Lesson_2_3 : - double literals
Lesson_2_3 : - unsigned literals
Lesson_2_3 : - various size int literals

/' ========== Escape characters ========== '/
Lesson_2_3_1 : - new line character
Lesson_2_3_1 : - backspace character
Lesson_2_3_1 : - tabulation character
Lesson_2_3_1 : - carriage return character

/' ========== Type deduction ========== '/
Lesson_2_3_2 : - auto
Lesson_2_3_2 : - deduction based on literals
Lesson_2_3_2 : - declaration by initialization
Lesson_2_3_2 : - auto and string literals
Lesson_2_3_2 : - std::initializer_list
Lesson_2_3_2 : - trailing return type notation

/' ========== String ========== '/
Lesson_2_4 : - std::string
Lesson_2_4 : - std::cin for std::string
Lesson_2_4 : - std::getline() for std::string

/' ========== String searching ========== '/
Lesson_2_4_1 : - std::string::find()
Lesson_2_4_1 : - std::string::npos

/' ========== String modification ========== '/
Lesson_2_4_2 : - string concatenation
Lesson_2_4_2 : - std::string::substr()
Lesson_2_4_2 : - std::stringstream

/' ========== Advanced output ========== '/
Lesson_2_5 : - #include <format>
Lesson_2_5 : - std::format()
Lesson_2_5 : - std::print()
Lesson_2_5 : - std::println()
Lesson_2_5 : - format string
Lesson_2_5 : - format specifiers

/' ========== Compile-time evaluation ========== '/
Lesson_2_6 : - constexpr
Lesson_2_6 : - consteval

/' ========== Basic math ========== '/
Lesson_3 : - int vs float
Lesson_3 : - basic int math
Lesson_3 : - basic float math
Lesson_3 : - mixing int and float in math
Lesson_3 : - modulo division

/' ========== Advanced floating-point ========== '/
Lesson_3_1 : - IEEE754
Lesson_3_1 : - rounding precision
Lesson_3_1 : - numeric stability

/' ========== Conditionals ========== '/
Lesson_4 : - if statement
Lesson_4 : - boolean type
Lesson_4 : - switch case
Lesson_4 : - preincrementation
Lesson_4 : - postincrementation

/' ========== Implicit bool conversions ========== '/
Lesson_4_1 : - evaluating numbers as bool
Lesson_4_1 : - evaluating characters as bool

/' ========== Compile-time conditionals ========== '/
Lesson_4_2 : - if constexpr

/' ========== Iterations ========== '/
Lesson_5 : - for loop
Lesson_5 : - while loop
Lesson_5 : - do while loop

/' ========== Static arrays ========== '/
Lesson_6 : - raw array
Lesson_6 : - std::array<>
Lesson_6 : - ranged for
Lesson_6 : - std::string as an array

/' ========== Advanced static arrays ========== '/
Lesson_6_1 : - C-string
Lesson_6_1 : - multidimensional raw arrays
Lesson_6_1 : - multidimensional std::array<>

/' ========== Functions ========== '/
Lesson_7 : - making a function
Lesson_7 : - function body
Lesson_7 : - parameters
Lesson_7 : - returning a value
Lesson_7 : - early return
Lesson_7 : - recursion

/' ========== Advanced functions ========== '/
Lesson_7_1 : - function prototype
Lesson_7_1 : - function overloading
Lesson_7_1 : - Tail Recursion Optimization (TRO)
Lesson_7_1 : - Return Value Optimization (RVO)
Lesson_7_1 : - inline functions
Lesson_7_1 : - default parameters
Lesson_7_1 : - constexpr functions

/' ========== Scopes ========== '/
Lesson_7_2 : - local scope
Lesson_7_2 : - global scope

/' ========== Side effects ========== '/
Lesson_7_3 : - pure functions
Lesson_7_3 : - static variables

/' ========== Splitting code into files ========== '/
Lesson_8 : - header files
Lesson_8 : - source files
Lesson_8 : - #include in detail
Lesson_8 : - #pragma once
Lesson_8 : - function prototypes in header files
Lesson_8 : - function bodies in source files

/' ========== In-depth codebase structure ========== '/
Lesson_8_1 : - compilation process
Lesson_8_1 : - translation units
Lesson_8_1 : - linking
Lesson_8_1 : - forward declarations

/' ========== External libraries ========== '/
Lesson_8_1_1 : - static libraries
Lesson_8_1_1 : - dynamic libraries

/' ========== Linking errors ========== '/
Lesson_8_1_2 : - symbol missing in translation unit
Lesson_8_1_2 : - missing library
Lesson_8_1_2 : - duplicated symbols

/' ========== Managing compiler optimizations ========== '/
Lesson_8_1_3 : - volatile
Lesson_8_1_3 : - compiler attributes

/' ========== Integration with C code ========== '/
Lesson_8_1_4 : - extern "C"

/' ========== Macros ========== '/
Lesson_8_2 : - preprocessor directives
Lesson_8_2 : - defines
Lesson_8_2 : - conditional compilation
Lesson_8_2 : - include guards vs #pragma once

/' ========== Modules ========== '/
Lesson_8_3 : - modules
Lesson_8_3 : - exporting symbols
Lesson_8_3 : - importing modules

/' ========== Enumeration types ========== '/
Lesson_9 : - enum
Lesson_9 : - scoped enum

/' ========== In-depth enums ========== '/
Lesson_9_1 : - enum base type
Lesson_9_1 : - assigning values to enum elements
Lesson_9_1 : - casting enums
Lesson_9_1 : - conversion functions for enums

/' ========== Structures ========== '/
Lesson_10 : - std::fstream
Lesson_10 : - std::getline with files
Lesson_10 : - std::stoi, std::stof, std::stod


Lesson_10_1 : - overloading stream operator
Lesson_10_1 : - std::filesystem
Lesson_10_1 : - binary files

/' ========== Structures ========== '/
Lesson_11 : - structures
Lesson_11 : - nesting structures
Lesson_11 : - brace initialization
Lesson_11 : - brace initialization with\n   explicit field names
Lesson_11 : - dot operator

/' ========== Default values ========== '/
Lesson_11_1 : - default field values
Lesson_11_1 : - brace initialization vs\n   default values

/' ========== Structure data access ========== '/
Lesson_11_2 : - aggregates
Lesson_11_2 : - structure methods
Lesson_11_2 : - structured binding

/' ========== Structure memory concerns ========== '/
Lesson_11_3 : - memory alignment
Lesson_11_3 : - padding
Lesson_11_3 : - bit fields

/' ========== In-depth look into structures ========== '/
Lesson_11_4 : - access modifiers (public, private)
Lesson_11_4 : - struct default access

/' ========== Unions ========== '/
Lesson_11_5 : - union
Lesson_11_5 : - std::variant<>
Lesson_11_5 : - undefined behavior\n   of unions

/' ========== Namespace ========== '/
Lesson_12 : - namespaces
Lesson_12 : - name collisions

/' ========== Anonymous namespaces ========== '/
Lesson_12_1 : - anonymous namespaces
Lesson_12_1 : - file-restricted visibility

/' ========== Variables ========== '/
Lesson_13 : - raw pointers
Lesson_13 : - references
Lesson_13 : - universal references
Lesson_13 : - name of a raw array as a pointer
Lesson_13 : - pointer function parameters
Lesson_13 : - reference function parameters
Lesson_13 : - arrow operator

/' ========== Variables ========== '/
Lesson_13_1 : - reinterpret_cast<>
Lesson_13_1 : - dynamic_cast<>
Lesson_13_1 : - C-style cast

/' ========== Variables ========== '/
Lesson_13_2 : - universal pointer
Lesson_13_2 : - pointer to function
Lesson_13_2 : - memory ownership
Lesson_13_2 : - memory ownership transfer
Lesson_13_2 : - pointer arithmetic

/' ========== Variables ========== '/
Lesson_14 : - std::unique_ptr<>
Lesson_14 : - std::shared_ptr<>
Lesson_14 : - std::weak_ptr<>
Lesson_14 : - std::vector<>
Lesson_14 : - std::list<>
Lesson_14 : - new operator
Lesson_14 : - delete operator
Lesson_14 : - delete[] operator

/' ========== Variables ========== '/
Lesson_14_1 : - stack
Lesson_14_1 : - heap
Lesson_14_1 : - contiguous memory
Lesson_14_1 : - non-contiguous memory
Lesson_14_1 : - memory fragmentation
Lesson_14_1 : - random memory access

/' ========== Variables ========== '/
Lesson_14_2 : - begin() method
Lesson_14_2 : - end() method
Lesson_14_2 : - iterators
Lesson_14_2 : - using iterators in for loop
Lesson_14_2 : - iterating over non-contiguous memory

/' ========== Variables ========== '/
Lesson_14_3 : - buffers
Lesson_14_3 : - placement new
Lesson_14_3 : - cache-friendly programming

/' ========== Variables ========== '/
Lesson_14_4 : - std::optional<>
Lesson_14_4 : - accessing optional value
Lesson_14_4 : - value_or()

/' ========== Variables ========== '/
Lesson_15 : - classes
Lesson_15 : - default constructors
Lesson_15 : - parametric constructors
Lesson_15 : - destructors
Lesson_15 : - methods
Lesson_15 : - fields
Lesson_15 : - RAII

/' ========== Variables ========== '/
Lesson_15_1 : - default keyword
Lesson_15_1 : - class method generation rules
Lesson_15_1 : - Rule of Zero

/' ========== Variables ========== '/
Lesson_15_2 : - move semantics
Lesson_15_2 : - assignment operator
Lesson_15_2 : - move assignment operator
Lesson_15_2 : - Rule of Five
Lesson_15_2 : - .push_back() vs .emplace_back() in std::vector<>

/' ========== Variables ========== '/
Lesson_16 : - encapsulation
Lesson_16 : - access specifiers (private, public)
Lesson_16 : - default class access
Lesson_16 : - getters
Lesson_16 : - setters

/' ========== Variables ========== '/
Lesson_17 : - static members
Lesson_17 : - static methods
Lesson_17 : - scope operator
Lesson_17 : - friend classes
Lesson_17 : - friend functions

/' ========== Variables ========== '/
Lesson_17_1 : - structured-binding-compliant interface
Lesson_17_1 : - custom iterators
Lesson_17_1 : - custom begin() and end() method
Lesson_17_1 : - custom cbegin() and cend() method
Lesson_17_1 : - custom rbegin() and rend() method

/' ========== Variables ========== '/
Lesson_17_2 : - class member pointer
Lesson_17_2 : - class method pointer

/' ========== Variables ========== '/
Lesson_18 : - what const object implies for methods
Lesson_18 : - const methods

/' ========== Variables ========== '/
Lesson_18_1 : - explicit constructors
Lesson_18_1 : - constexpr constructors
Lesson_18_1 : - std::initializer_list
Lesson_18_1 : - initializer list constructor
Lesson_18_1 : - default parameters in constructors
Lesson_18_1 : - multiple parametric constructors
Lesson_18_1 : - private constructors
Lesson_18_1 : - delegating object construction\n   to a static method
Lesson_18_1 : - construction guards

/' ========== Advanced const objects properties ========== '/
Lesson_18_2 : - volatile members inside const objects

/' ========== Variables ========== '/
Lesson_19 : - protected access specifier
Lesson_19 : - public inheritance
Lesson_19 : - protected inheritance
Lesson_19 : - private inheritance
Lesson_19 : - name shadowing
Lesson_19 : - accessing private parent members
Lesson_19 : - inheritance also possible with structs
Lesson_19 : - protected also applying to structs

/' ========== Variables ========== '/
Lesson_19_1 : - multiple inheritance
Lesson_19_1 : - diamond problem
Lesson_19_1 : - accessing member of a specific parent

/' ========== Variables ========== '/
Lesson_20 : - what is polymorphism
Lesson_20 : - virtual functions
Lesson_20 : - abstract classes
Lesson_20 : - purely virtual functions
Lesson_20 : - virtual destructors
Lesson_20 : - method overloading
Lesson_20 : - operator overloading
Lesson_20 : - override
Lesson_20 : - final

/' ========== Variables ========== '/
Lesson_20_1 : - vtable
Lesson_20_1 : - dynamic_cast
Lesson_20_1 : - rules for downcasting

/' ========== Variables ========== '/
Lesson_20_2 : - overloading new operator
Lesson_20_2 : - overloading delete operator
Lesson_20_2 : - overloading delete[] operator
Lesson_20_2 : - conversion operators
Lesson_20_2 : - functors
Lesson_20_2 : - rules for implicit conversion\n   of custom types

/' ========== Variables ========== '/
Lesson_20_3 : - type aliases
Lesson_20_3 : - namespace aliases
Lesson_20_3 : - using type
Lesson_20_3 : - using namespace
Lesson_20_3 : - decltype

/' ========== Variables ========== '/
Lesson_20_4 : - creational patterns
Lesson_20_4 : - structural patterns
Lesson_20_4 : - behavioral patterns
Lesson_20_4 : - singleton using static function

/' ========== Variables ========== '/
Lesson_21 : - exceptions
Lesson_21 : - #include <stdexcept>
Lesson_21 : - try / catch blocks

/' ========== Variables ========== '/
Lesson_21_1 : - static_assert
Lesson_21_1 : - assert
Lesson_21_1 : - noexcept
Lesson_21_1 : - custom exceptions
Lesson_21_1 : - different handling for\n   different exceptions

/' ========== Variables ========== '/
Lesson_22 : - teplates
Lesson_22 : - template full specialization
Lesson_22 : - template partial specialization
Lesson_22 : - templates simplified with auto

/' ========== Variables ========== '/
Lesson_22_1 : - decltype and return type\n   based on template parameters
Lesson_22_1 : - variadic templates
Lesson_22_1 : - parameter pack
Lesson_22_1 : - caching using templates

/' ========== Variables ========== '/
Lesson_22_2 : - std::enable_if
Lesson_22_2 : - std::declval
Lesson_22_2 : - type_traits library
Lesson_22_2 : - CRTP - Curriously\n   Recurring Template Pattern
Lesson_22_2 : - SFINAE - Substitution Failure\n   Is Not An Error
Lesson_22_2 : - std::decay
Lesson_22_2 : - concepts

/' ========== Variables ========== '/
Lesson_22_3 : - template rules regarding linking
Lesson_22_3 : - template forward declarations
Lesson_22_3 : - moving class template\n   method definitions to source files

/' ========== Variables ========== '/
Lesson_23 : - std::pair<>
Lesson_23 : - std::tuple<>
Lesson_23 : - std::make_tuple<>
Lesson_23 : - std::tie
Lesson_23 : - std::map<>
Lesson_23 : - std::unordered_map<>
Lesson_23 : - std::set<>
Lesson_23 : - std::unordered_set<>
Lesson_23 : - std::find
Lesson_23 : - std::ranges::find

/' ========== Variables ========== '/
Lesson_23_1 : - chrono
Lesson_23_1 : - random
Lesson_23_1 : - iosfwd

/' ========== Variables ========== '/
Lesson_23_2 : - Boost::ASIO
Lesson_23_2 : - Qt
Lesson_23_2 : - OpenGL
Lesson_23_2 : - Vulkan
Lesson_23_2 : - CUDA
Lesson_23_2 : - PhysX

/' ========== Variables ========== '/
Lesson_24 : - lambda
Lesson_24 : - lambda capture block
Lesson_24 : - lambda aggregate capture specifiers
Lesson_24 : - std::find_if
Lesson_24 : - std::ranges::find_if
Lesson_24 : - std::ranges::remove_if
Lesson_24 : - std::ranges::for_each
Lesson_24 : - algorithm library

/' ========== Variables ========== '/
Lesson_24_1 : - function pointer
Lesson_24_1 : - std::function<>
Lesson_24_1 : - callbacks

/' ========== Variables ========== '/
Lesson_24_2 : - std::views<>
Lesson_24_2 : - std::ranges::view<>
Lesson_24_2 : - std::transform
Lesson_24_2 : - std::filter
Lesson_24_2 : - lazy evaluation

/' ========== Variables ========== '/
Lesson_25 : - threads
Lesson_25 : - parallelism
Lesson_25 : - concurrency

/' ========== Variables ========== '/
Lesson_25_1 : - thread priority
Lesson_25_1 : - scheduler
Lesson_25_1 : - preemption
Lesson_25_1 : - thread blocking
Lesson_25_1 : - thread yielding

/' ========== Variables ========== '/
Lesson_25_2 : - asynchronous operations
Lesson_25_2 : - coroutines
Lesson_25_2 : - ISR - Interrupt Service\n   Routine

/' ========== Variables ========== '/
Lesson_26 : - critical section
Lesson_26 : - semaphore
Lesson_26 : - mutex
Lesson_26 : - scoped lock
Lesson_26 : - blocking queue
Lesson_26 : - polling

/' ========== Variables ========== '/
Lesson_26_1 : - atomic instructions
Lesson_26_1 : - #include <atomic>
Lesson_26_1 : - atomic types

/' ========== Variables ========== '/
Lesson_27 : - deadlock
Lesson_27 : - thread starvation
Lesson_27 : - race condition

/' ========== Variables ========== '/
Lesson_27_1 : - main function parameters
Lesson_27_1 : - signal handler
Lesson_27_1 : - system calls
Lesson_27_1 : - thread vs process
@enduml
```