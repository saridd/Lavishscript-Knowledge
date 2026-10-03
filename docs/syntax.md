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
 
## IF Statements
 
Single statement:
 
```lavishscript
if ${Condition}
return TRUE
```
 
Block:
 
```lavishscript
if ${Condition}
{
echo "Success"
return TRUE
}
```
 
---
 
## WHILE
 
```lavishscript
while ${Count} < 10
{
Count:Inc
}
```
 
---
 
## DO/WHILE
 
```lavishscript
do
{
}
while ${Iterator:Next(exists)}
```
 
---
 
## Return Values
 
```lavishscript
return TRUE
```
 
```lavishscript
return "${PlayerName}"
```
 
```lavishscript
return 123
```
