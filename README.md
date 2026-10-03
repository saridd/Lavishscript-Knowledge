# Lavishscript-Knowledge

A structured knowledge base for LavishScript, InnerSpace, ISXEQ2, and project-specific automation patterns.
 
This repository serves four purposes:
 
1. Preserve working LavishScript patterns.
2. Document language behavior and common pitfalls.
3. Capture project architecture and debugging history.
4. Improve AI-assisted development using GitHub Copilot and similar tools.
 
---
 
# Audience
 
This repository is intended for:
 
- LavishScript developers
- InnerSpace developers
- ISXEQ2 developers
- GitHub Copilot users
- Future maintainers of these automation projects
 
---
 
# Repository Structure
 
```text
docs/
├── lavishscript/
├── innerspace/
├── isxeq2/
└── projects/
 
examples/
├── relay/
├── json/
├── iterators/
└── objectdefs/
```
 
---
 
# Documentation Areas
 
## LavishScript
 
Language syntax and behavior.
 
Topics include:
 
- Variables
- Functions
- Object definitions
- Iterators
- JSON
- Events
- Return values
- Common pitfalls
 
---
 
## InnerSpace
 
Runtime architecture and communication.
 
Topics include:
 
- Sessions
- Relay
- RelayByRef
- Script execution
- Variable scopes
- Session management
 
---
 
## ISXEQ2
 
EverQuest II integration.
 
Topics include:
 
- Equipment scanning
- Loot windows
- Actors
- Group members
- Datatypes
- Item information
 
---
 
## Project Documentation
 
Each significant project should maintain:
 
- Architecture
- Design decisions
- Testing notes
- Known issues
- Changelog
 
---
 
# Principles
 
## Proven Patterns First
 
Examples should be based on code that has been tested and proven to work.
 
---
 
## Document Bugs
 
Significant bugs should be documented together with:
 
- Root cause
- Symptoms
- Fix
- Prevention
 
---
 
## Small Examples
 
Prefer small focused examples over large scripts.
 
Good:
 
```lavishscript
call GetLootItemDetails 1
echo ${Return}
```
 
Less useful:
 
```lavishscript
1500 lines of unrelated script
```
 
---
 
# Current Projects
 
## LootDistribute
 
Automated EQ2 treasure chest allocation system.
 
Current architecture:
 
```text
Loot Window
↓
RefreshPlayerStats
↓
QueryEquipment
↓
TransmitPlayer
↓
ReceivePlayer
↓
PlayerInfoStore
↓
ChooseRecipient
↓
AssignLootItem
```
 
---
 
# Contributions
 
When documenting a new discovery:
 
1. Capture the problem.
2. Capture the root cause.
3. Capture the working solution.
4. Provide a minimal example.
 
Knowledge should be reusable.
