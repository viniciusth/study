Data files or primary files can be implemented in three ways:
#### Index Organized Tables
Stores data records in the files themselves.
Range scans can be implemented as a sequential scan on the files due to index.
#### Heap Organized Tables
Don't follow any particular order, most of the time data is written in order.
Heap files require extra additional index structures pointing to object locations so data can be fetched efficiently.
#### Hash Organized Tables
Data is stored in buckets, the hash value of the key determines which bucket the data belongs to.
Data inside the bucket may be sorted to support indexing or unsorted.
