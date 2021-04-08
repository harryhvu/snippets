### Dependencies
`import openpyxl`

### Data Types
- object
- int64
- float64
- bool
- datetime64
- timedelta[ns]
- category

### Creating DataFrames
From objects/dictionaries

```
class Signal(object):
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def to_dict(self):
        return {
            'x': self.x,
            'y': self.y,
        }
        
signals = [Signal(3, 9), Signal(4, 16)]

pandas.DataFrame.from_records([s.to_dict() for s in signals])
```

From Fixed Width File in .txt format (FWF)
```
df = pd.read_fwf('filename.txt')
```

From html (make sure variable is string)
```
table = soup.find_all('table')
df = pd.read_html(str(table))[0]
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


### Filtering
Filtering using `.loc`
```
df = df.loc[(df['column name'] == 'value')]
```
- You can use multiple filters in one line by separating the filters in parentheses with '&'

Filter Out NaN Values
```
combined_df = combined_df[combined_df.End_Date.notnull()]
```

Filter - keep rows based on list of strings
```
df = df[df['your column'].isin(['list of strings'])]
```
- or use ~ if you want to drop rows


Keep rows with specific string
```
df_rld = df[df['col_name'].str.contains('string_here')]
```

Drop empty columns or rows
```
df = df.dropna(axis=0,how='all')
```
- pass 0 for rows and 1 for columns in 'axis'

### Indexing by a Datetime Column
- First set index to a column with datetime objects
- Then reference using something like `df['2019']`
```
df.set_index(df['Dates'])
df['2019']
```

### Sorting
` df_by_price_type = df_by_price_type.sort_values(by='Effective_Date')`
 

### Get list of unique values in a column
`df_name_here['col name'].unique()`


### Get first or last row of dataframe (can replace tail with head)
```
pd.concat([df.head(1), df.tail(1)])
```

### Dataframe Metadata, Labeling Columns, Indexes
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

Rename column
```
df.rename({'col_name':'new_col_name'})
```

Reset index
```
df.reset_index(drop=True)
```

## Adding Data or Columns

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
 
Split 1 column and create 2 new ones from it
```
Split 1 column into 2 and add the 2 new columns to the dataframe
df[['First','Last']] = df.Name.str.split("_",expand=True)
```

Creating a new column with df.assign()
```
Split 1 column into 2 and add the 2 new columns to the dataframe
df[['First','Last']] = df.Name.str.split("_",expand=True)
```

Assign list of values to a column
```
df = df.assign(columnamehere=lambdafunctionorvalue)
```

Merge strings across columns in a row
```
df['new col'] = df['colA'] + df['colB']
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
```
df.read_csv('filename.csv', dtype = {'col name': 'category'})
```

### Change data type for a column
```
df['Application No.'] = pd.to_numeric(df['Application No.'])
```

### Convert strings to numbers (if col has correct data type eg not a combo of strings and numbers)
## Can also use with 'category' to convert float to string
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

## Descriptive Statistics and Aggregation

Using .groupby() and then .resample()
```
def summary_grpbydrug_resample(df):
    df = df.groupby('Nam_drug').resample('A-JUN').agg({'Amt Paid Final':'sum','Num Icn':'count','Recip ID':'nunique'})

    return df
```
- .resample() can be called after .groupby()

Get descriptive statistics (eg min, max, mean, std, etc)
```
df['column_name'].describe()
```
- you can also use the describe method on the entire dataframe with `df.describe(include='all')`

Count occurences of each value in a column
```
df['column'].value_counts()
```

Count unique values
```
def beneficaries_bystc(df):
    df = df.groupby('Dsc_thera_cls_spec')[['Recip ID']].nunique()

    return df
```
Get Descriptive Statistics
`df.describe()`

Resampling A Column (in other words, grouping data by time)
```
df = df['col_to_aggregate'].resample('Q').mean()
```
- you need the name of the column that will be aggregated, the "frequency string" (e.g. Q), and the aggregating method (e.g. mean() )
- you also have to convert the datetime column to datetime objects?
- also set your datetime column as the index


Resampling a Data Frame with Different Aggregation Functions
```
def claims_test_resample_df(df):
    df['Hdr Fdos'] = pd.to_datetime(df['Hdr Fdos'])
    df = df.set_index(df['Hdr Fdos'])
    df = df.resample('A').agg({'Num Icn':'count','Amt Paid Final':'sum'}) # how to aggregate different columns with diff aggregation functions

    return df
    
```

Aggregate data with different aggregation methods for each column
```
df.groupby('A').agg({'B': ['min', 'max'], 'C': 'sum'})
```

Get the minimum value across rows (axis=0) or columns (axis=1)
```
df.min(axis=1
```

Get the minimum value column label across rows (axis=0) or columns (axis=1)
```
df.idxmin(axis=1)
```

### Lambda and custom functions

Assign value to new column from value in another column using anonymous lambda function or custom function
```
df['newcol'] = df['oldcol'].apply(lambda x: myfunction(x))
or
df['newcol'] = df['oldcol'].apply(lambda x: x-1)
```

## Miscellaneous
Replacing values in a column (e.g. replacing 0 with NaN)
```
reference_cod_smac['smac'] = reference_cod_smac['smac'].replace(0,np.NaN)
```




