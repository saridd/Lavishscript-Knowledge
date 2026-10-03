# Iterators
 
## Standard Pattern
 
```lavishscript
variable iterator Iterator
 
Collection:GetIterator[Iterator]
 
if ${Iterator:First(exists)}
{
do
{
}
while ${Iterator:Next(exists)}
}
```
 
---
 
## Nested Iterators
 
Example:
 
```lavishscript
if ${Iterator.Value.FirstKey(exists)}
{
do
{
}
while ${Iterator.Value.NextKey(exists)}
}
```
 
---
 
## Common Usage
 
Loot member processing.
 
Class rank processing.
 
JSON key enumeration.
