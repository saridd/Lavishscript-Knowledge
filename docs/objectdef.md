# Object Definitions
 
## Example
 
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
 
## Methods
 
Methods do not return through `${Return}`.
 
Example:
 
```lavishscript
Example:Reset
```
 
---
 
## Members
 
Members return values.
 
Example:
 
```lavishscript
echo ${Example.Value}
```
 
---
 
## Typical Usage
 
```lavishscript
PlayerInfoStore:Clear
 
echo ${PlayerInfoStore.HasPlayer[Ajiark]}
```
