# Arrays library.

Basic (associative) array functions.

## A. Functions.

note(s):
* all functions in this section have action and patch variants, coded via `DEFINE_DIMORPHIC_FUNCTION`.

`is_key_in_array STR_VAR array key RET bool`

Return true if `key` is a key of `array`, false otherwise.  The `array` is passed by name.

note(s):
* this is O(1) since it can be reduced to a variable set check. The underlying check is *I think*, O(log_2(n)), because OCaml implements arrays as binary trees.

`get_array_count STR_VAR array RET count`

Return the number of pairs `key => value` in the `array`. The `array` is passed by name.

note(s):
* this is O(n) since must loop through the array to count the entries.

`get_array_element STR_VAR default = "*" array key RET value`

Return the `value` associated to `key` in `array`. The advantage of this function in comparison with simply

```
$"%array%"("%key%")
```

is that it will automatically return `default` if `key` is not in `array`instead of returning garbage (e.g. un-expanded string).

`find_key STR_VAR value array default = "*" RET key`

Return the first key whose value matches `value`. Returns `default` (defaulting to "*") if no match is found.

note(s):
* different keys can match the same value and the first key returned depends on the iteration order of `ACTION_PHP_EACH`; because of this, this function is useful only if it is guaranteed that the association keys -> values is injective.

`find_all_keys STR_VAR value associations RET_ARRAY array`

Return the array of all keys whose associated value matches `value`. Returns empty array if no match is found.
