# Generic library.

A utilities library to handle the processing of all sorts of binary format files.

file(s):

* [Source code](../../generic.tpa).

# A. Builders.

`load_offsets_table STR_VAR file = "" RET_ARRAY table`

Load offsets table; this is a specialized version of `load_table` for relative offsets tables used by `get_field` and `set_field` functions.

# B. Generic reader and writer.

`get_field_at INT_VAR offset STR_VAR field offsets RET value`

Generic read function. Return the value of `field` relative to `offset` using `offsets`table. If `field` is not a valid field, function PATCH_FAIL's.

note(s):
* casing of `field` is irrelevant.

`set_field_at INT_VAR offset STR_VAR field value offsets`

Generic write function. Write `value`, passed as a string, to `field` relative to `offset` using `offsets` table. If `field` is not a valid field, function PATCH_FAIL's.

note(s):
* casing of `field` is irrelevant.
