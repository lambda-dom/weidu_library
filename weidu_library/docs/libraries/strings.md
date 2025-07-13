# Strings.

A library containing some basic string manipulation functions.

file(s):

* [Source code](../../strings.tpa).

# A. Functions.

note(s):
* all functions in this section have action and patch versions.

`strip_left STR_VAR value RET string`

Strip all whitespace (spaces and tab characters) of string `value` from the left.

`strip_right STR_VAR value RET string`

Strip all whitespace (spaces and tab characters) of string `value` from the right.

`strip STR_VAR value RET string`

Strip all whitespace (spaces and tab characters) of string `value` from both ends.

# B. From strings to lists.

`get_chars STR_VAR value RET count RET_ARRAY list`

Return the `list` of characters of `value` string.
