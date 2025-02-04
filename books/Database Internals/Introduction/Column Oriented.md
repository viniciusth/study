- Stores fields of different rows in order
- Efficient for fetching or operating over individual fields.
- Good for analytical workloads
#### Wide Column Stores
- Introduces the concept of column families: Columns families store multiple versions of data by timestamp.
- Column families store each entry for the same row sequentially sorted by timestamp, this makes it quick to find data related to a row and which versions it had over time.


#flashcards/DatabaseInternals/Introduction 

What access patterns make column oriented DB's faster than row oriented?::When queries span many rows or compute aggregates of a subset of columns.

What are column families in Wide Column Stores?::They are the method for storing data, in which row history is saved. Entries are sorted by row id and their version timestamp.