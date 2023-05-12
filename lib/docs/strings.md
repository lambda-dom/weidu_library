# Strings library.

Basic string manipulation functions.

## A. Functions.

note(s):
* all functions in this section have action and patch variants (coded via `DEFINE_DIMORPHIC_FUNCTION`).

`repeat_string INT_VAR times = 1 STR_VAR string RET_ARRAY strings`

Return array with string `string` as element repeated `times`. Function PATCH_FAIL's if `times` is 0 or negative.

`join_strings STR_VAR strings sep = " " RET string`

Joins all elements in the 0-indexed array `strings` into one string, with individual elements separated by `sep` (defaults to single space). If array has 0 elements, returns the empty string.
