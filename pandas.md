### Dependencies
import openpyxl

### Creating DataFrames
From html (make sure variable is string)
```
table = soup.find_all('table')
df = pd.read_html(str(table))[0]
```

##From excel
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

### Filtering
Filter - out empty fields where 'End Date' is column name
`combined_df = combined_df[combined_df.End_Date.notnull()]`

Filter - Drop rows based on list of strings
`df = df[~df['your column'].isin(['list of strings'])]`

Filter - Keep rows with a certain value e.g 2299 or you can use != to filter out 2299
`combined_df = combined_df[combined_df.End_Date_Year == 2299]`

Keep rows with specific string
```
df_rld = df[df['col_name'].str.contains('string_here')]
```

Drop empty columns or rows
df = df.dropna(axis=0,how='all')
- pass 0 for rows and 1 for columns in 'axis'

### Sort
 df_by_price_type = df_by_price_type.sort_values(by='Effective_Date')
 
### Concatenate dfs
pd.concat(list_of_dfs)

### Split Columns
```
Split 1 column into 2 and add the 2 new columns to the dataframe
df[['First','Last']] = df.Name.str.split("_",expand=True)
```

### Get list of unique values in a column
df_name_here.column_name_here.unique()

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

### Get info about dataframe
Shape - returns (#,#)
`df.shape`

### Number of columns
`columns_count = len(df.columns)`

### Get number of rows in dataframe
`len(combined_df.index)`

### Rename column
`df.rename({'col_name':'new_col_name'})`

### Reset index
`df.reset_index(drop=True)`

##Changing Data

### Fill in non-numerical values with 'NaN'
`pd.to_numeric(df.col_name, errors='coerce')`

### Fill 'NaN' with zeros instead
pd.to_numeric(df.col_name, errors='coerce').fillna(0)

### Reduce dataframe size when reading
cols = [ list of column names you want to read ]
df = pd.read_csv(data, usecols=cols)

### Specify data type before reading
dtypes = {'col name': 'category'}

### Convert strings to numbers (if col has correct data type eg not a combo of strings and numbers)
`df.astype({'col_name':'float'}).dtypes`


