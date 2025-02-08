#databases
- [x] recall what you can, then reread and adjust


![[books/Database Internals/Architecture]]

### Decisions
DBMS's can have many different architectural choices 
- [[books/Database Internals/Row oriented]] vs [[books/Database Internals/Column Oriented]]
- [[books/Database Internals/Disk Based DB]] vs [[books/Database Internals/Memory Based DB]]
Other important concepts: [[books/Database Internals/Data files]] and [[books/Database Internals/Index files]].
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
