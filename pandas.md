# Creating DataFrames
data = list of lists
df = pd.DataFrame(data)

Assign lists to columns
df = pd.DataFrame(columns=['col_name1','col_name2']
df['col_name1'] = list_variable
df['col_name2'] = list_variable

# Filtering
Filter - out empty fields where 'End Date' is column name
combined_df = combined_df[combined_df.End_Date.notnull()]

Filter - Drop rows based on list of strings
df = df[~df['your column'].isin(['list of strings'])]

Filter - Keep rows with a certain value e.g 2299 or you can use != to filter out 2299
combined_df = combined_df[combined_df.End_Date_Year == 2299]

# Sort
 df_by_price_type = df_by_price_type.sort_values(by='Effective_Date')

# Split Columns
Split 1 column into 2 and add the 2 new columns to the dataframe
df[['First','Last']] = df.Name.str.split("_",expand=True) 

# Get number of rows in dataframe
(len(combined_df.index))

# Get list of unique values in a column
df_name_here.column_name_here.unique()

# Exporting 
dataframe to excel
final_df.to_excel('final_df.xlsx')

# Get first or last row of dataframe (can replace tail with head)
pd.concat([df.head(1), df.tail(1)])
