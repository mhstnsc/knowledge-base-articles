# filtering
 * dataframe - `df[df[<column>] > 0]`
 * dataframe - `df.query('column > 0 && column2 < 0')`
 * dataframe - `df[df['column'].isin(elements)]`
 * series - `s[s > 0]`
 * group data - `df.groupby('A').filter(lambda x: x['bla'].mean() > 0)` <- filter groups

# map
 * group data - `df.groupby('column').apply(lambda df: f(df, df.name)) -> DataFrame`; df.name passes the value of the grouping 
 * map over a column - `df['column'].apply(lambda v: ...) -> Series`
 * map over each row - `df.apply(lambda series: ...., axis=1) -> series

# sorting

 * data-frame - `df.sort_values([column1, columns2], ascending=[true,false])`. It can also apply a key function for index sorting, sort in place with `inplace`
 * group-data - `df.groupby(...).apply(lambda x: x.sort_values(..))` - sorting a group

# iterating 
 * data frame iteration
    ```
    for index, row in df.iterrows():
      row['column1']
    ```
  * 
# selecting rows

 * dataframe - selecting row by index - `df.iloc[10] -> Series` -> `row['column']`, `df[start:end]`
 * dataframe - selecting row by key
   ```
   idx = df.set_index(["col1","col2"])
   row = idx.loc[("val_col1", "val_col2")]
   row["col3"]
   ```
 * groups - select a group - `df.groupby(...).get_group(<name>) -> DataFrame`

# selecting columns
 * by name: `df["column"]` or `df[["col1", "col2"]]`


# combining
 * join `pd.merge(df1, df2, on=['column', 'column'])`
 * concet `pd.concat(df1, df2)`

# sampling
 * `df.sample(n=8)`
    


