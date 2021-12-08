# sorting

 * `pd.sort_values([column1, columns2], ascending=[true,false]). It can also apply a key function for index sorting, sort in place with `inplace`
 * `pd.groupby(...).apply(lambda x: x.sort_values(..))` - sorting a group
