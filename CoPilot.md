Copilot Instructions
This repository contains LavishScript code for InnerSpace and ISXEQ2.

Use LavishScript conventions and syntax exclusively.

Language Requirements
Use:

LavishScript
InnerSpace
ISXEQ2
Do not assume:

C#
Python
JavaScript
Lua
PowerShell
syntax applies.

Function Calls
Functions are called with:

call FunctionName argument1 argument2
Return values are accessed via:

${Return}
Example:

call GetLootSlot primary

echo ${Return}
Variable Scope
Variables are function-scoped.

They are NOT block-scoped.

Incorrect:

while ${Condition}
{
    variable string Name
}
Correct:

variable string Name

while ${Condition}
{
}
IF Statements
Single statements are valid:

if ${Condition}
    return TRUE
However braces are preferred:

if ${Condition}
{
    return TRUE
}
Never assume multiple indented lines belong to an IF.

Bad:

if ${Condition}
    echo Test
    return FALSE
Good:

if ${Condition}
{
    echo Test
    return FALSE
}
Object Definitions
Use:

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
JSON Usage
Preferred datatypes:

jsonvalue
jsonvalueref
Use:

SetReference
SetByRef
Merge
patterns already present in repository examples.

Relay Architecture
Preferred session communication pattern:

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
Debugging Standard
Debug output should follow:

echo "DEBUG: Message"
Examples:

echo "DEBUG: LootResolve=${LootResolve}"

echo "DEBUG: BestPlayer=${BestPlayer}"
ISXEQ2 Development
Assume:

LootWindow exists
Me datatypes exist
Equipment datatypes
