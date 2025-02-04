- Most common type of orientation used to store data.
- Data for a entry is stored sequentially, thus it is better for use cases where usually we read most of the row in queries. This makes it easier to create rows as well since the data can be inserted directly.
- Makes queries accessing individual fields of multiple different rows slower.


#flashcards/DatabaseInternals/Introduction 

What access patterns make row oriented DB's faster than column oriented?::When most columns of a row are returned by queries