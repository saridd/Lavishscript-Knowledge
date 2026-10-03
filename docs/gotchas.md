# Gotchas
 
## Variables Are Function Scoped
 
Most common source of runtime bugs.
 
---
 
## IF Statements
 
Without braces only the next statement belongs to the IF.
 
Bad:
 
```lavishscript
if ${Condition}
echo "Fail"
return FALSE
```
 
Good:
 
```lavishscript
if ${Condition}
{
echo "Fail"
return FALSE
}
```
 
---
 
## Function Returns
 
Functions return via:
 
```lavishscript
${Return}
```
 
Not through method syntax.
 
---
 
## LootDistribute Lessons Learned
 
### ChosenLooter
 
Declared inside loop.
 
Result:
 
```text
Variable named 'ChosenLooter' already exists in scope
```
 
Fix:
 
Declare outside loop.
 
### Relay Verification
 
Always validate:
 
```text
TransmitPlayer
ReceivePlayer
ReceivedPlayerCount
```
 
before debugging allocator logic.
