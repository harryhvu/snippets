## Text files
### Creating a text file
`txt = open('file_name.txt','a+')`

### Saving a text file after creating it
`txt.close()`

### Writing
`txt.write()`

### Reading
```
with open('sections.txt','r') as file:
  data = file.read()
```

### All Access Modes
- Read Only (‘r’) : Open text file for reading. The handle is positioned at the beginning of the file. If the file does not exists, raises I/O error. This is also the default mode in which file is opened.
- Read and Write (‘r+’) : Open the file for reading and writing. The handle is positioned at the beginning of the file. Raises I/O error if the file does not exists.
- Write Only (‘w’) : Open the file for writing. For existing file, the data is truncated and over-written. The handle is positioned at the beginning of the file. Creates the file if the file does not exists.
- Write and Read (‘w+’) : Open the file for reading and writing. For existing file, data is truncated and over-written. The handle is positioned at the beginning of the file.
- Append Only (‘a’) : Open the file for writing. The file is created if it does not exist. The handle is positioned at the end of the file. The data being written will be inserted at the end, after the existing data.
- Append and Read (‘a+’) : Open the file for reading and writing. The file is created if it does not exist. The handle is positioned at the end of the file. The data being written will be inserted at the end, after the existing data.

## Get Today's Date
```
from datetime import date
today = date.today()
```

## Flatten a list of lists
non_flat is the list of lists
x is each sublist in the list of lists
` flat_list = [y for x in non_flat for y in x] `

## .replace() with multiple characters
```
a_string = "breads"
remove_characters = ["e", "s"]

for character in remove_characters:
    a_string = a_string.replace(character, "")
```
## Iterate over files in a directory
https://stackoverflow.com/questions/10377998/how-can-i-iterate-over-files-in-a-given-directory

