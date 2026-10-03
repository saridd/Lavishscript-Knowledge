# Copilot Instructions
 
This repository contains LavishScript code for InnerSpace and ISXEQ2.
 
Use LavishScript conventions and syntax exclusively.
 
---
 
# Language Requirements
 
Use:
 
- LavishScript
- InnerSpace
- ISXEQ2
 
Do not assume:
 
- C#
- Python
- JavaScript
- Lua
- PowerShell
 
syntax applies.
 
---
 
# Function Calls
 
Functions are called with:
 
```lavishscript
call FunctionName argument1 argument2
```
 
Return values are accessed via:
 
```lavishscript
${Return}
```
 
Example:
 
```lavishscript
call GetLootSlot primary
 
echo ${Return}
```
 
---
 
# Variable Scope
 
Variables are function-scoped.
 
They are NOT block-scoped.
 
Incorrect:
 
```lavishscript
while ${Condition}
{
variable string Name
}
```
 
Correct:
 
```lavishscript
variable string Name
 
while ${Condition}
{
}
```
 
---
 
# IF Statements
 
Single statements are valid:
 
```lavishscript
if ${Condition}
return TRUE
```
 
However braces are preferred:
 
```lavishscript
if ${Condition}
{
return TRUE
}
```
 
Never assume multiple indented lines belong to an IF.
 
Bad:
 
```lavishscript
if ${Condition}
echo Test
return FALSE
```
 
Good:
 
```lavishscript
if ${Condition}
{
echo Test
return FALSE
}
```
 
---
 
# Object Definitions
 
Use:
 
```lavishscript
objectdef Example
{
method Reset()
{
}
 
member:int Value()
{
return 1
}
}
```
 
---
 
# JSON Usage
 
Preferred datatypes:
 
```lavishscript
jsonvalue
jsonvalueref
```
 
Use:
 
```lavishscript
SetReference
SetByRef
Merge
```
 
patterns already present in repository examples.
 
---
 
# Relay Architecture
 
Preferred session communication pattern:
 
```text
Coordinator
↓
relay
↓
Remote Client
↓
QueryEquipment
↓
TransmitPlayer
↓
RelayByRef
↓
ReceivePlayer
```
 
---
 
# Debugging Standard
 
Debug output should follow:
 
```lavishscript
echo "DEBUG: Message"
```
 
Examples:
 
```lavishscript
echo "DEBUG: LootResolve=${LootResolve}"
 
echo "DEBUG: BestPlayer=${BestPlayer}"
```
 
---
 
# ISXEQ2 Development
 
Assume:
 
- LootWindow exists
- Me datatypes exist
- Equipment datatypes
