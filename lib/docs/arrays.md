# Arrays library.

Basic (associative) array functions.

Note that because of the way WeiDU treats arrays as bundles of variables, checking if an array has a given key is fraught with problems. The check

```
VARIABLE_IS_SET $array("%key%")
```

will return a false positive if the variable `array_%key%` is set. Therefore, to be safe, one must loop through the array and extract what one wants which is O(n).

## A. Functions.

note(s):
* all functions in this section have action and patch variants, coded via `DEFINE_DIMORPHIC_FUNCTION`.
* in all functions requiring string comparisons, comparison is *case insensitive*.

`is_key_in_array STR_VAR array key RET bool`

Return true if `key` is a key of `array`, false otherwise. The `array` is passed by name.

`get_array_count STR_VAR array RET count`

Return the number of pairs `key => value` in the `array`. The `array` is passed by name.

note(s):
* this is O(n) since must loop through the array to count the entries.

`get_array_element STR_VAR default = "*" array key RET value`

Return the `value` associated to `key` in `array`. The advantage of this function in comparison with simply

```
$"%array%"("%key%")
```

is that it will automatically return `default` if `key` is not in `array` instead of returning garbage (e.g. un-expanded string). The disadvantage is that it is O(n) because it must loop through the array.

`find_key STR_VAR value array default = "*" RET key`

Return the first key whose value matches `value`. Returns `default` (defaulting to "*") if no match is found.

note(s):
* different keys can match the same value and the first key returned depends on the iteration order of `ACTION_PHP_EACH`; because of this, this function is mostly useful if it is guaranteed that the association `keys => values` is injective or alternatively you have sorted the keys via something like a call to `SORT_ARRAY_INDICES`.

`find_all_keys STR_VAR value associations RET_ARRAY array`

Return the array of all keys whose associated value matches `value`. Returns the empty array if no match is found.
