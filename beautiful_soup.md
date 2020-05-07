### Importing the module
`from bs4 import BeautifulSoup`

### Creating soup
`soup = BeautifulSoup(r.content,'lxml')`
`soup = BeautifulSoup(r.text,'xml')`

### Get list of all tags by tag name
Find by tag name
`h1_list = soup.find_all('h1')`

### Find tags with specific attribute (eg class) and value ('subheading')
`h1 = soup.find('h1',attrs={'class':'subheading'})`

### Get value of attribute (eg 'href') inside HTML element (eg '<a>')
```
atags = soup.find_all('a')
for atag in atags:
  url = atag['href']
 ```
  
### Find element with specific string inside
if 'string' in str(soup_object):
  do this

  
