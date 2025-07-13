# Tables library.

Basic table (.2da files) manipulation functions.

file(s):

* [Source code](../../tables.tpa).

# A. Builders.

note(s):
* all functions in this section have action and patch versions.

This is a variation of WeiDU's `READ_2DA_ENTRY_FORMER` loading the entire table into an array, plus (internal, undocumented) entry for metadata, like the number of rows. The table is then maniputaed with the table manipulation functions detailed below.

`load_table STR_VAR file fields RET_ARRAY table`

This function loads the entire .2da `file` (full path) into an associative array `table` where each entry is indexed by the row and field, where row is an integer and field is an element from the `:`-separated list `fields` constructed via `list_from_string` from the [Lists library](./lists.md). The function FAIL's if the number of columns in the table is not equal to the number of fields. Uniqueness of fields in the `fields` list is *not* checked; if this condition is not met the returning array will be malformed.

Once the table is loaded into an array, use the usual array indexing, e.g. assuming `array` is the array's name:

```weidu
OUTER_TEXT_SPRINT entry $array("%row%" "%field%")
```

Better than using direct indexing, is to use the table manipulation functions -- see section below.

note(s):
* if the 2da file has 2 columns and its header is something like the usual 2da header "2DA V1.0", the array returned will have extra entries. This is a bug in the WeiDU parser. To avoid such a problem, make sure the file has no header and no named columns, just the data rows.

# B. Basic table functions.

All these functions manipulate arrays produced by `load_table`. If any other type of arrays is fed to it, garbage is returned.

note(s):
* all functions in this section have both patch and action functions.

`get_table_row_count STR_VAR table RET count`

Return the number of rows in `table`, a table passed by name. The function FAIL's if `table` does not have the table format.

`get_table_fields STR_VAR table RET fields`

Return the `:`-separated list of fields of the table. Will return garbage if `table` does not have the table format.

`get_row_from_table INT_VAR row STR_VAR table RET_ARRAY array`

Return the `row` array from `table`. The function FAIL's if `table` does not have the table format or if `row` is out of bounds.

# C. Linear searches.

`find_table_row STR_VAR table field key RET index`

Return `index` of (first) row of `table` containing `key` in column `field`, -1 if not found. Comparisons are case-insensitive, string comparisons.

# D. Array builders.

`array_from_table STR_VAR table key value RET_ARRAY array`

Builds an (associative) array from the `table`. The keys are the values in column `key` and the associated values are the values in the column `value`.
