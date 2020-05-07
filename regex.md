### Search between two strings
```
txt = "Startstring of sentence 123 blah blah blah endstring 123"
x = re.search(r"Startstring.*?123", txt)
match = x.group()

output: "Startstring of sentence 123"
```
or
```
txt = "Startstring of sentence 123 blah blah blah endstring 123"
x = re.search(r"Startstring.*123", txt)
match = x.group()

output: "Startstring of sentence 123 blah blah blah endstring 123"
```
