# LootDistribute Debugging History

This document captures significant issues encountered during the development of LootDistribute, their root causes, and proven fixes.

---

# Architecture Overview

```text
Loot Window
    ↓
GetLootItemDetails
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

# Debugging Session: LootDistribute V2/V3

## Issue: Script Compiled But Did Nothing

### Symptoms

```text
Script started
No parse errors
No loot assigned
```

### Investigation

Added debug tracing throughout:

```lavishscript
echo "DEBUG: SCRIPT STARTED"
echo "DEBUG: Session=${Session}"
echo "DEBUG: CoordinatorSession=${CoordinatorSession}"
```

### Outcome

Confirmed script was entering:

```text
main()
RefreshPlayerStats()
```

but failing later in the execution path.

---

## Issue: ClassRanks Validation Failure

### Symptoms

```text
ERROR: ClassRanks must contain exactly 26 class ranks.
```

### Investigation

Instrumented:

```lavishscript
ValidateClassRanks()
```

to dump all configured class ranks.

### Root Cause

Validation logic was functioning correctly.

The issue was uncertainty around configuration loading.

Additional debug proved:

```text
ClassRanks exists = TRUE
RankCount = 26
```

### Resolution

ClassRanks configuration confirmed valid.

No code change required.

---

## Issue: ChosenLooter Variable Scope Error

### Symptoms

```text
Variable named 'ChosenLooter' already exists in scope
Could not add variable named 'ChosenLooter'
Main function call failed
```

### Root Cause

LavishScript variables are function-scoped.

The following declaration was inside a loop:

```lavishscript
variable string ChosenLooter
```

Each loop iteration attempted to recreate it.

### Fix

Move declaration outside loop.

Incorrect:

```lavishscript
while ${LootWindow.NumItems} > 0
{
    variable string ChosenLooter
}
```

Correct:

```lavishscript
variable string ChosenLooter

while ${LootWindow.NumItems} > 0
{
}
```

### Lesson

Variables are not block-scoped.

---

## Issue: RefreshPlayerStats Waited Forever

### Symptoms

```text
Waiting. Received=0/5
```

Coordinator never progressed.

### Investigation

Added tracing around:

```lavishscript
relay
TransmitPlayer
ReceivePlayer
```

### Root Cause

Initially appeared to be a relay failure.

Further investigation showed:

```text
ReceivePlayer
```

was executing correctly.

### Resolution

Relay system confirmed working.

---

## Issue: ReceivePlayer Verification

### Investigation

Added instrumentation:

```lavishscript
echo "DEBUG: ReceivePlayer ENTERED"
```

### Result

Confirmed:

```text
QueryEquipment
↓
TransmitPlayer
↓
RelayByRef
↓
ReceivePlayer
↓
ReceivedPlayerCount++
```

was functioning correctly.

### Lesson

Always verify relay callbacks before investigating allocator logic.

---

## Issue: Gedola Missing From Verification

### Symptoms

```text
ReceivedPlayerCount=5

ERROR:
no complete fresh equipment scan was received
for loot recipient 'Gedola'
```

### Investigation

Added logging inside:

```lavishscript
VerifyPlayerScans()
```

and

```lavishscript
ReceivePlayer()
```

### Resolution

Player relay and storage logic verified.

Subsequent testing confirmed scans were being received properly.

---

## Issue: LootResolve Always Appeared As Zero

### Symptoms

```text
FOUND RESOLVE

LootResolve=0
```

even though item inspection showed:

```text
Resolve = 165
```

### Investigation

Added debugging to:

```lavishscript
GetLootItemDetails()
```

### Findings

Correctly detected:

```text
Modifier 10
SubType='Resolve'
Value='165.000000'
```

and:

```text
LootItemPriorityStat=165
```

### Root Cause

Incorrect value was being passed into:

```lavishscript
ChooseRecipient()
```

### Resolution

Confirmed correct parameter flow:

```text
LootItemPriorityStat=165
↓
CurrentItemResolve=165
↓
ChooseRecipient(...)
↓
LootResolve=165
```

### Lesson

Verify values at every boundary between functions.

---

## Issue: Unable To Determine Why Ajiark Was Selected

### Symptoms

Logs showed:

```text
ChooseRecipient returned 'Ajiark'
```

However:

```text
DefaultLooter='Ajiark'
```

making it impossible to determine whether:

- Ajiark won
- DefaultLooter was used

### Resolution

Added explicit return-path logging.

```lavishscript
RETURNING DEFAULT
```

and

```lavishscript
RETURNING BEST PLAYER
```

### Outcome

Confirmed:

```text
RETURNING BEST PLAYER Keliax
```

and the allocator was functioning correctly.

---

## Issue: Assignment Appeared To Fail

### Symptoms

```text
assignment did not remove item from window
```

### Investigation

Reviewed in-game behaviour.

Observed:

```text
Item selected
Recipient selected
Assign clicked
```

### Root Cause

Testing was intentionally interrupted to allow reuse of the same treasure chest.

The assignment validation message was expected.

### Resolution

No allocator bug present.

---

# Proven Working Components

## Configuration

```text
LoadAllocatorConfiguration
ValidateClassRanks
```

Verified.

---

## Player Collection

```text
GetLootMemberList
QueryEquipment
TransmitPlayer
ReceivePlayer
PlayerInfoStore
```

Verified.

---

## Loot Analysis

```text
GetLootItemDetails
Resolve Detection
Class Filtering
```

Verified.

---

## Recipient Selection

```text
ChooseRecipient
Class Ranking
Upgrade Evaluation
```

Verified.

Example:

```text
LootResolve=165

BestPlayer='Keliax'

RETURNING BEST PLAYER Keliax
```

---

## Assignment

```text
Item Selection
Dropdown Selection
LeaderAssign Click
```

Verified.

---

# Key LavishScript Lessons Learned

## Variables Are Function Scoped

Most expensive bug encountered during development.

Always declare reusable variables outside loops.

---

## Use Explicit Debug Logging

Debug output should show:

```text
Entry
Input
Decision
Output
```

for every major function.

---

## Verify Data At Function Boundaries

Example:

```text
GetLootItemDetails
↓
CurrentItemResolve
↓
ChooseRecipient
```

Never assume values passed correctly.

Always log them.

---

# Future Investigation

The next area for validation is:

```text
Player equipment resolve values
```

to ensure:

```text
BestResolve
```

is being calculated from actual equipped item data rather than default or zero values.
