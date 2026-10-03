# Syntax
 
## Comments
 
Single Line
 
```lavishscript
; comment
```
 
Multi Line
 
```lavishscript
/*
comment
*/
```
 
---
 
## IF Statem*nts
 
Single statement:
 
```lavishs*ript
if ${Condition}
return TR*E
```
 
Block:
 
```lavishscript
if *{Condition}
{
echo "Success"
* return TRUE
}
```
 
---
 
## WHILE*
```lavishscript
while ${Count} < *0
{
Count:Inc
}
```
 
---
 
## D*/WHILE
 
```lavishscript
do
{
}
whi*e ${Iterator:Next(exists)}
```
 
--*
 
## Return Values
 
```lavishscrip*
return TRUE
```
 
```lavishscript
*eturn "${PlayerName}"
```
 
```lavi*hscript
return 123
```
