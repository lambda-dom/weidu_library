# The Ids library

A library to ease getting values out of .ids files.

file(s):

* [Source code](../../ids.tpa).

# A. Basic functions.

note(s):
* all functions in this section have patch and action variants.

`get_id_from_ids STR_VAR ids value RET id`

Return the integer `id` associated to `value` in ids resource `ids`. If `ids` is not a valid ids file or `id` not in the ids file, return `-1`.

note(s):
* casing of `id` or `ids` are irrelevant.
* in the case of non-existent `ids` file, WeiDU logs an error.

`get_ids_from_id INT_VAR id STR_VAR ids RET value`

Return the symbolic `value` associated to the numeric `id` in the `ids` file. If `ids` is not a valid ids file the function FAIL's and if no value is associated to `id`, the function returns `*`.

note(s):
* casing of `ids` is irrelevant.
* in the case of non-existent `ids` file, WeiDU logs an error.
