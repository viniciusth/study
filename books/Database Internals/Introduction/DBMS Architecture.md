#databases
- [x] recall what you can, then reread and adjust


![[books/Database Internals/Introduction/Architecture]]

### Decisions
DBMS's can have many different architectural choices 
- [[Row oriented]] vs [[Column Oriented]]
- [[Disk Based]] vs [[Memory Based]]
Other important concepts: [[Data files]] and [[Index files]].
### Definitions for DBMS
#### Transaction Manager
Schedules transactions, ensures logically consistent state.
#### Lock Manager
Locks objects for transaction usage, ensures physical data integrity.
#### Access Methods
Manage access and data organization. ex: [[B Trees]], [[LSM Trees]]
#### Buffer Manager
Caches data pages in memory
#### Recovery Manager
Maintains operation logs and restores system state in case of failures
#### Buffering
#### Immutability
#### Ordering
