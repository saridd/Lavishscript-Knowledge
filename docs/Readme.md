# LavishScript Reference
 
This section documents LavishScript language behavior,
InnerSpace patterns, and proven development practices.
 
## Purpose
 
This documentation exists to:
 
- Preserve working knowledge.
- Improve Copilot assistance.
- Reduce repeated debugging.
- Document language pitfalls.
- Provide reusable patterns.
 
## Topics
 
### Language
 
- Syntax
- Variables
- Functions
- Object Definitions
- Iterators
 
### Runtime
 
- Relay
- Sessions
- JSON
- Debugging
 
### Best Practices
 
- Proven design patterns
- Known pitfalls
- Common fixes
 
## Important Rules
 
Functions return values through:
 
```lavishscript
${Return}
```
 
Variables are:
 
```text
Function Scoped
```
 
NOT:
 
```text
Block Scoped
```
 
Always prefer braces for multi-line IF statements.
