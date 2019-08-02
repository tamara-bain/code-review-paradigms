## Code Review Checklist

A summary of code review standards produced from the research by [The Institude for Software Quality](http://www.ifsq.org).
Here is a checklist of things your code should not contain before putting it up for code review. 

### 1. Routine too long - [SP-1](http://www.ifsq.org/indicator-SP-1.html):
Code blocks should not be longer than 150 lines. Keep files and classes as short as possible and if neccesary break out classes into a module of several files.

### 2. Too much nesting - [SP-2](http://www.ifsq.org/finding-sp-2-a.html)
Nesting and conditional statements should never exceed 3 levels and should ideally only be one level. 

### 3. No magic numbers or strings (DRY) - [SPM-1](http://www.ifsq.org/indicator-SPM-1.html), 
Magic numbers (other than 0, or 1) increase the time to make maintenance changes and increase risk of error. Use constants instead.

### 4. No magic strings in control flow (DRY) - [SPM-2](http://www.ifsq.org/indicator-SPM-2.html)
Any if/while/and/or that involves magic strings should have the strings refactored into constants.

### 5. No copy and paste programming (DRY) - [SPM-3](http://www.ifsq.org/indicator-SPM-3.html)
Sections of identical or almost identical code in two or more places increases maintenance time and errors because you now have to maintain logic in multiple places. 

### 6. Control flow complexity - [SP-3](http://www.ifsq.org/indicator-SP-3.html)
More than 10 control flow statements (if/while/until/and/or) can indicate a program is too complex. Complex functions are harder to maintain, test and cause errors. 10 is the upper bounds. Fewer control flow statements is better. 

### 7. Errors are caused during communication between routines, especially external routines - [DP-1](http://www.ifsq.org/indicator-DP-1.html), [DP-2](http://www.ifsq.org/indicator-DP-2.html)
40% of errors are caused by errors occuring when passing/receiving data between functions/classes/modules. Explictly check that values are present and within the expected range (either through type checking, or asserts) when working with external interfaces or in delicate/error prone functions. Errors (try/catch) should always be handled, specific, and documented.

### 8. Dangling if statements - [DB-3](http://www.ifsq.org/indicator-DP-3.html)
Check for any if/else statement that does not cover all cases. Research shows this is a hot spot for errors where the default case should be handled in a particular way. 

### 9. WIP - [WIP-1](http://www.ifsq.org/indicator-WIP-1.html), [WIP-2](http://www.ifsq.org/indicator-WIP-2.html)
Any TODOs left in the code should be explicit about WHAT needs to be done and WHEN it needs to be done. No dead code (commented out lines, code after return statements) should remain in production (this can be checked into a branch and removed if it needs to be documented). No unused variables should remain in production.

### 10. Cohesive - [SP-4](http://www.ifsq.org/indicator-SP-4.html)
Modules and classes should be cohesive - related content should be grouped together and unrelated content should be refactored into it's own class or module. Things should be where you expect them to be. 

### 11. Naming - [SP-5](http://www.ifsq.org/indicator-SP-5.html)
Names should be descriptive without being too long. They should be clearly differentiated from other names in the code block. Ideal names for debugging average 10-16 characters long.

### 12. Standard Patterns
Effort should be made to follow best practices of the language or framework and existing structure in the code base. Avoid doing things that are specifically recommended against by the framework or language. This reduces friction for other people editing/maintaining your code because it reads in a style they are familiar with. It also reduces the likelyhood that changes in packages/frameworks interfere with our codebase. 

### 13. Efficiency
Do things with reasonable efficiency for 10x our current level of growth. Avoid premature optimization unless the effort to do so is identical to not doing so. This should prevent anything grossly inefficient from getting into our codebase without adding unneccessary complexity. 


## Perspectives of a Code Review

These are perspectives to read through the code with after completing the above assessment. 

### Not complete
Read through the code looking for completeness. Does the program cover everything it is supposed to do? Is there any feature missing? (hotspots: analytics, error reporting, uptime monitoring, async. tasks, caching)

### Wrong result
Read through the code looking for correctness. Is there anything in the program that could give the wrong result? Are calculations correct? Is the control flow logic correct? Is the business logic correct? 

### Hard to maintain
Read through the code imagining yourself maintaining it. Is there anything that would be difficult to maintain? Is there anything that is confusing or hard to remember? Would it be hard to refactor or change in the future? Will it create inefficiencies that will interfere with the operation of the program?
