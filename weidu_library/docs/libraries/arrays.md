# Arrays library.

Functions for manipulating (associative) arrays.

note(s):
* in all functions requiring comparisons, unless explicitly said otherwise, comparisons are of strings and _case insensitive_.

file(s):

* [Source code](../../arrays.tpa).

# A. Basic functions.

note(s):
* all functions in this section have action and patch variants.

`get_array_count STR_VAR array RET count`

Return the `count` of pairs `key => value` in the `array`. The `array` is passed by name.

note(s):
* this function is linear in the size of the array, since must loop through it to count the entries.

# B. Linear searches.

note(s):
* all functions in this section have action and patch variants.

`get_array_element STR_VAR array key default = "*" RET value`

Return the `value` associated to `key` in `array`. The advantage of this function in comparison with simply

```weidu
$"%array%"("%key%")
```

is that it will automatically return `default` if `key` is not in `array` instead of returning garbage (e.g. un-expanded string). This is because WeiDU treats arrays as bundles of variables referenced with name mangling; therefore the check

```weidu
VARIABLE_IS_SET $array("%key%")
```

will return a false positive if the variable `array_%key%` is set. This means that `get_array_element` is linear in the size of the array, since it has to loop through it to find the correct value. To make matters worse, the only way to break out of the loop early when a match is found, is by raising an exception and then catch it.

`is_key_in_array STR_VAR array = "" key = "" RET bool`

Return true if `key` is in `array`.

`find_key STR_VAR array value default = "*" RET key`

Return the first key whose value matches `value`. Returns `default` (defaulting to "*") if no match is found.

note(s):
* different keys can match the same value and the first key returned depends on the iteration order of `ACTION_PHP_EACH`; because of this, this function is mostly useful if it is guaranteed that the association `keys => values` is injective, or alternatively, you have sorted the keys via say, a call to `SORT_ARRAY_INDICES`.

`find_all_keys STR_VAR value array RET count RET_ARRAY list`

Return the `list` of all `key`'s of `array` whose value matches `value`. Returns the empty list if no match is found.

# C. Builders.

note(s):
* all functions in this section have action and patch variants.

`array_from_keys STR_VAR keys value = "*" RET_ARRAY array`

Return a new associative array with pairs `key => value` with keys the elements of the list of `keys` and values `value`.

note(s):
* repeated `key`'s are merged into a single pair, so this is one way to extract the unique elements (unique with respect to case-insensitive, string comparison) of a list.

`enumerate_list STR_VAR keys RET_ARRAY array`

Return a new associative array with pairs `key => value` with keys the elements of the list of `keys` and values their indices.

`merge_arrays STR_VAR arrays RET_ARRAY array`

Merge `arrays` passed by name as a `|`-separated stringified list. If there are common keys, the last one wins.

`load_array INT_VAR col = 1 STR_VAR table RET_ARRAY array`

Builds an array from the `table` file (full path) and a column index. The keys are the values in the first column and the values are the values in the `col` column. This function implicitly assumes the keys are unique.

note(s):
* if the 2da file has 2 columns and its header is something like the usual 2da header `2DA V1.0`, the array returned will have extra keys. This is a bug in the WeiDU parser. To avoid such a problem, this case is treated especially, and the `2DA` key is _not_ introduced.
