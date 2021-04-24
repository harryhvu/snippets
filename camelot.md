## Camelot Snippets

### Reading the pdf
```
import camelot
tables = camelot.read_pdf('filename.pdf', pages='1-end')
```

### Concattenating tables - list comprehension to convert to dfs then concat
```
dfs = [table.df for table in tables]
merged_dfs = pd.concat(dfs)
```

