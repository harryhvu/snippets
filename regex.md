### Search between two strings
```
txt = "Startstring of sentence blah blah blah endstring"
x = re.search("^Startstring.*endstring$", txt)
match = x.group()
```
or
```
txt = "Startstring of sentence blah blah blah endstring"
x = re.search("Startstring.*?endstring", txt)
match = x.group()
```
