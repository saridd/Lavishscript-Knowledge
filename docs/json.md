JSON
 
## Datatypes
 
```lavishscript
jsonvalue
jsonvalueref
```
 
---
 
## SetReference
 
```lavishscript
joPlayer:SetReference["{}"]
```
 
---
 
## SetByRef
 
```lavishscript
joStorage:SetByRef[player,joPlayer]
```
 
---
 
## Merge
 
```lavishscript
joPlayer:Merge["Context.Get[player]"]
```
 
---
 
## Common Pattern
 
```lavishscript
joPlayer:SetReference[
"joStorage.Get[\"${playerName~}\"]"
]
```
