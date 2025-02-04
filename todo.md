#### Pending Tasks
```dataview
TASK where status = " " group by file.path sort file.mtime asc
```
#### TODO Notes
```dataview
LIST file.path from #todo sort file.mtime asc
```