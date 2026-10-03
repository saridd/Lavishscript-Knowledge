# Functions
 
## Definition
 
```lavishscript
function GetValue()
{
return 123
}
```
 
---
 
## Calling Functions
 
```lavishscript
call GetValue
```
 
Access result:
 
```lavishscript
echo ${Return}
```
 
---
 
## Parameters
 
```lavishscript
function Add(int A, int B)
{
return ${Math.Calc[${A}+${B}]}
}
```
 
Call:
 
```lavishscript
call Add 2 3
```
 
Result:
 
```lavishscript
echo ${Return}
```
 
---
 
## Typical Pattern
 
```lavishscript
call GetLootSlot primary
 
if ${Return} < 0
{
echo "Error"
}
```
