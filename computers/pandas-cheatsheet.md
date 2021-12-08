# filtering
 * `df[df[<column>] > 0]`
 * `df.query('column > 0 && column2 < 0')`
 * `s[s > 0]`

# sorting

 * `df.sort_values([column1, columns2], ascending=[true,false])`. It can also apply a key function for index sorting, sort in place with `inplace`
 * `df.groupby(...).apply(lambda x: x.sort_values(..))` - sorting a group
