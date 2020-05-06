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
