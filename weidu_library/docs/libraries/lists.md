# List functions.

List functions.

note(s):
* WeiDU does not make a distinction between lists and arrays, with lists just being associative arrays with (contiguous, integer) indices.

file(s):

* [Source code](../../lists.tpa).

# A. Basic functions.

note(s):
* all functions in this section have action and patch variants.

`get_list_count STR_VAR list RET count`

Return the `count` of elements in the `list`.

# B. Builders.

note(s):
* all functions in this section have action and patch variants.

`repeat_string INT_VAR times STR_VAR value RET_ARRAY list`

Return `list` of string `value` as element repeated `times`. Function FAIL's if `times` is negative and returns the empty list if `times` is 0.

`list_from_string STR_VAR string separator = "," RET count RET_ARRAY list`

Creates a `list` from a `separator`-separated `string`. `separator` must be 1-character long, otherwise function FAIL's, and the element strings are stripped of surrounding whitespace.

# C. Folds.

`join_strings STR_VAR strings separator = " " RET string`

Specialized fold that joins all elements in the 0-indexed array `strings` into one string, with individual elements separated by `separator` defaulting to a single space character. If array has 0 elements, returns the empty string.
