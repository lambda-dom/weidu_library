# 2da library.

Various functions to directly manipulate .2da table files. Usually it is more efficient to load the entire table with `load_table`, but when patching (e. g. engine game tables) this is not feasible because serialization code is only available through `SET_2DA_ENTRY_LATER` and `SET_2DA_ENTRIES_NOW`.

file(s):

* [Source code](../../2da.tpa).

# A. Linear searches.

note(s):
* all functions in this section are patch functions for table `.2da` files, and other files with the same tabular structure like `.ids` files.

`find_column_index STR_VAR key RET index`

Returns the (first) column index corresponding to key in the row of names whose value is `key`, -1 if it does not exist. Comparison of strings is case-insensitive.

`find_row_index INT_VAR col = 0 start = 0 STR_VAR key RET index`

Return the index of the first row whose column `col` value is `key`, in the 2da file, -1 if it does not exist. Search starts at `start` (defaults to 0). Comparison of strings is case-insensitive.

note(s):
* the code does *not* correct the index when the table has 2 columns.

`find_row_index_from_end INT_VAR col = 0 end = -1 STR_VAR key RET index`

Return the index of the first row whose column `col` value is `key`, in the 2da file, -1 if it does not exist. Search starts at `end` (defaulting to the last row) and proceeds backwards towards the start.

note(s):
* the code does *not* correct the index when the table has 2 columns.

`find_all_rows INT_VAR col = 0 STR_VAR key RET_ARRAY indexes`

Return an array of all row indices with `col` entry matching `key`.
