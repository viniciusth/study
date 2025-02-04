- Data is primarily stored in-memory, disk is mostly used for recovery and logging.
- Accessing memory is several orders of magnitude faster than accessing disk.
- Memory is still more expensive than disk.
- Programming for main memory is simpler than programming for disk.
- In-memory data suffer from lack of durability due to RAM volatility.
- For recovery, results are usually written to a sequential log file and used as [[Write-ahead logs]]


#flashcards/DatabaseInternals/Introduction

What is the biggest issue with memory based DBMS's?::Lack of durability