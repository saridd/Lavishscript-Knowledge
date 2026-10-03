# Relay Patterns
 
## Architecture
 
Coordinator
 
```text
RefreshPlayerStats
```
 
Remote
 
```text
QueryEquipment
```
 
Communication
 
```text
TransmitPlayer
↓
RelayByRef
↓
ReceivePlayer
```
 
## Proven Working Sequence
 
```text
QueryEquipment
TransmitPlayer
RelayByRef
ReceivePlayer
ReceivedPlayerCount++
```
 
## Debug Checklist
 
Verify:
 
1. QueryEquipment executes.
2. TransmitPlayer executes.
3. RelayByRef sends.
4. ReceivePlayer fires.
5. ReceivedPlayerCount increments.
