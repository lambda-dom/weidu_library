# Tables library.

Basic table (.2da files) manipulation functions.

## A. Builders.

note(s):
* all functions in this section have patch and action versions, coded via `DEFINE_DIMORPHIC_FUNCTION`.

`build_array_from_2da INT_VAR col = 1 STR_VAR table dir = "*" RET_ARRAY array`

Builds an associative array from the table file and a column index. The keys are the values in the first column (0-indexed) and the values are the values in the `col` column. This function implicitly assumes the keys are unique. If `dir` is not provided, the table file is looked up in component's resources 2da dir.

note(s):
* if the 2da file has 2 named columns or less and its header is something like the usual 2da header "2DA V1.0", the array returned will have extra keys. This is a bug in the WeiDU parser. To avoid such a problem, make sure the file has no header and no named columns, just the data rows.

## B. Search functions.

note(s):
* all functions in this section are patch functions.

`find_column_index STR_VAR key RET index`

Returns the (first) column index corresponding to key in the row of names whose value is `key`, -1 if it does not exist. Comparison of strings is case-insensitive.

`find_first_row INT_VAR col = 0 start = 0 STR_VAR key RET index`

Return the first row index whose column `col` value is `key`, in the 2da file, -1 if it does not exist. Search starts at `start` (defaults to 0). Comparison of strings is case-insensitive.

note(s):
* the code does *not* correct the index when the table has 2 columns and first row is "2DA". This is a bug in WeiDU's parser that should skip the signature line in table files.

`find_first_row_from_end INT_VAR col = 0 start = -1 STR_VAR key RET index`

The same function as `find_first_row` except it returns the first match with the search starting from the end.

`find_all_rows INT_VAR col = 0 STR_VAR key RET_ARRAY indexes`

Return an array of all row indexes with `col`entry matching `key`.

## C. Writers.

`append_row STR_VAR key = "" default = "*"`

Append a row to the end of the table with first column `key` and `default` values in the other columns.
