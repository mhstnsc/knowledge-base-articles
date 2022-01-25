# filtering
 * dataframe - `df[df[<column>] > 0]`
 * dataframe - `df.query('column > 0 && column2 < 0')`
 * series - `s[s > 0]`
 * group data - `df.groupby('A').filter(lambda x: x['bla'].mean() > 0)` <- filter groups

# map
 * group data - `df.groupby(...).apply(lambda df: ...) -> DataFrame`
 * map over a column - `df['column'].apply(lambda v: ...) -> Series`
 * map over each row - `df.apply(lambda series: ...., axis=1) -> series

# sorting

 * data-frame - `df.sort_values([column1, columns2], ascending=[true,false])`. It can also apply a key function for index sorting, sort in place with `inplace`
 * group-data - `df.groupby(...).apply(lambda x: x.sort_values(..))` - sorting a group

# iterating & selecting

 *  data frame iteration
    ```
    for index, row in df.iterrows():
      row['column1']
    ```
 * dataframe - selecting row by index - `df.iloc[10] -> Series` -> `row['column']`
 * dataframe - selecting row by key
   ```
   idx = df.set_index(["col1","col2"])
   row = idx.loc[("val_col1", "val_col2")]
   row["col3"]
   ```
 * groups - select a group - `df.groupby(...).get_group(<name>) -> DataFrame`

    


