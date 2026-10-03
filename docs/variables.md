# Variables
 
## Declaration
 
```lavishscript
variable int Count = 0
```
 
```lavishscript
variable bool Found = FALSE
```
 
```lavishscript
variable string Name = ""
```
 
---
 
## Scope Rules
 
Variables are function scoped.
 
They are NOT block scoped.
 
Bad:
 
```lavishscript
while ${Condition}
{
variable string ChosenLooter
}
```
 
Result:
 
```text
Variable named 'ChosenLooter' already exists in scope
```
 
Good:
 
```lavishscript
variable string ChosenLooter
 
while ${Condition}
{
}
```
 
---
 
## Global Variables
 
```lavishscript
variable(global) int Counter = 0
```
 
---
 
## Set()
 
```lavishscript
Name:Set["Steve"]
```
 
```lavishscript
Counter:Set[10]
```
