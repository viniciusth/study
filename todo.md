Some tables for when not sure what to do.
#### TODO Notes
```dataview
table file.path as Path from #todo sort file.mtime asc
```
#### Notes to revisit
```dataview
table file.path as Path, round((date(now) - file.mtime).days, 2) as "Days since modified" from #revisit sort file.mtime asc
```