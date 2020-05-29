### Dependencies
`import openpyxl`

### Creating DataFrames
From html (make sure variable is string)
```
table = soup.find_all('table')
df = pd.read_html(str(table))[0]
```

From excel
```
df = pd.read_excel('file.xlsx')
```

From list of lists where each list is a ROW
```
data = list of lists
df = pd.DataFrame(data)
```

From list of lists where ach list of a COLUMN
```
df = pd.DataFrame({
 'alerts':alerts,
 'alert_descriptions':alert_descriptions,
 'paid_amts':paid_amts,
 'reversed_amts':reversed_amts
 })
```

Assign lists to columns
```
df = pd.DataFrame(columns=['col_name1','col_name2']
df['col_name1'] = list_variable
df['col_name2'] = list_variable
```

build a dataframe from multiple files ROW WISE(eg multiple spreadsheets)
```
from glob import glob
files = sorted(glob('data/stocks*.csv'))
```
- looks for csv files starting with 'stocks' in the 'data' subdirectory
returns list of file names that are sorted

From clipboard
```
df = pd.read_clipboard()
pd.concat((pd.read_csv(file) for file in files), ignore_index=True)
```

### Filtering
Filter - out empty fields where 'End Date' is column name
```
combined_df = combined_df[combined_df.End_Date.notnull()]
```

Filter - Drop rows based on list of strings
```
df = df[~df['your column'].isin(['list of strings'])]
```

Filter - Keep rows with a certain value e.g 2299 or you can use != to filter out 2299
```
combined_df = combined_df[combined_df.End_Date_Year == 2299]
```

Keep rows with specific string
```
df_rld = df[df['col_name'].str.contains('string_here')]
```

Multiple filters and Keep rows with specific value or string
Use & for multiple filters
```
new_df = df.loc[(df['Type'] == 'value here'] & (df['Column 2'] > 1234)]
```

Drop empty columns or rows
```
df = df.dropna(axis=0,how='all')
```
- pass 0 for rows and 1 for columns in 'axis'


### Sort
` df_by_price_type = df_by_price_type.sort_values(by='Effective_Date')`
 
### Concatenate DataFrames
`pd.concat(list_of_dfs)`

### Split Columns
```
Split 1 column into 2 and add the 2 new columns to the dataframe
df[['First','Last']] = df.Name.str.split("_",expand=True)
```

### Get list of unique values in a column
`df_name_here['col name'].unique()`

### Exporting
```
dataframe to excel
import openpyxl
final_df.to_excel('final_df.xlsx')
```

### Get first or last row of dataframe (can replace tail with head)
```
pd.concat([df.head(1), df.tail(1)])
```

### Get info about DataFrame
Shape - returns (#,#)
```
df.shape
```

Number of columns
```
columns_count = len(df.columns)
```

Get number of rows in dataframe
```
len(combined_df.index)
```

### Rename column
`df.rename({'col_name':'new_col_name'})`

### Reset index
`df.reset_index(drop=True)`

## Changing Data

Adding new column/data based on conditional (contains a string)
```
    #dmd_key_words = ['DMD','duchenne','muscular','dystrophy'] # option 1
    #pattern = '|'.join(dmd_key_words)
    #df['Subject'] = df['Body'].str.contains(pattern) #returns True/False/NaN
```
```
    df.loc[df['Body'].str.contains('DMD|duchenne|muscular|dystrophy|duchennes'), 'DMD'] = 'True' # option 2 returns a customized value
    df.loc[df['Body'].str.contains('diabetes|dm|t2dm|diabetic'), 'DM'] = 'False'
 ```

Adding a new column
```
df['new col'] = list of values
```

Mapping - Create a new column if another column has dictionary key, return dictionary value
```
openfda_df['Indexed RLD'] = openfda_df['Application No.'].map(rld_dict)
```
- .map(dictionary_here)

### Convert strings to datetimes in a column
`df['col nam'] = pd.to_datetime(df['col name'])`
or
`pd.to_datetime(pd.Series(['05/23/2005']), format="%m/%d/%Y")`

### Fill in non-numerical values with 'NaN'
`pd.to_numeric(df.col_name, errors='coerce')`

### Fill 'NaN' with zeros instead
`pd.to_numeric(df.col_name, errors='coerce').fillna(0)`

### Reduce dataframe size when reading
```
cols = [ list of column names you want to read ]
df = pd.read_csv(data, usecols=cols)
```

### Specify data type before reading
`dtypes = {'col name': 'category'}`

### Change data type for a column
```
df['Application No.'] = pd.to_numeric(df['Application No.'])
```

### Convert strings to numbers (if col has correct data type eg not a combo of strings and numbers)
`df.astype({'col_name':'float'}).dtypes`

### Add values across rows from specific columns and create a new column with a total
`df['Total'] = df['col val 1'] + df['col val 2']`

## Selecting Data
.iloc
[row_num,column_num], colon (:) gives all rows
```
df.iloc[1,2]
df.iloc[:,0]
```

.loc
```
for i in range(len(df)) : 
  print(df.loc[i, "Name"], df.loc[i, "Age"])
```
- note that i is the row number (similar to .iloc)

### Analysis

Get descriptive statistics (eg min, max, mean, std, etc)
```
df['column_name'].describe()
```

Count occurences of each value in a column
```
df['column'].value_counts()
```

### Get Descriptive Statistics
`df.describe()`






