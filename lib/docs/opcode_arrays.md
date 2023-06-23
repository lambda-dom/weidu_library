# Opcode Arrays library.

A library to process opcodes using arrays.

For the purposes of this document an *opcode array* is an associative array with fields a, possibly proper, subset of the valid opcode fields. If a field has value `*` then it is treated as if it was not in the array.

## A. Array opcode functions.

note(s):
* all functions in this section are patch functions.

`get_opcode_array INT_VAR offset RET_ARRAY array`

Return the associative array of pairs `field => value` of opcode at `offset`.

`match_opcode_against_array INT_VAR offset = 0 STR_VAR array RET bool`

Matches opcode at `offset` field by field against the `array` fields. PATCH_FAIL's if any of the array fields is not an opcode field. Array `array` is passed by name.

note(s):
* casing of *both* fields and values in the array is irrelevant.

### A. 1. Writers.

`alter_opcode_with_array INT_VAR offset STR_VAR array`

Write the various opcode fields in `array` to opcode at `offset`. Only valid field names in `opcode_array` are considered. The function does error checking to avoid inserting garbage data as much as possible.

note(s):
* casing of array fields is irrelevant.

### A. 2. Builders.

note(s):
* all functions in this section have both patch and action variants, coded via `DEFINE_DIMORPHIC_FUNCTION`.
* casing of array fields is irrelevant.

`create_null_opcode_array RET_ARRAY array`

Return an opcode array with all values set to null, with the exception of `probability1` set to 100.

### A. 3. Utilities.

note(s):
* all functions in this section have both patch and action variants, coded via `DEFINE_DIMORPHIC_FUNCTION`.
* casing of array fields is irrelevant.

`convert_symbols_opcode_array STR_VAR opcode_array = "" RET_ARRAY array`

Convert any fields with symbolic values to their (numeric) counterparts. Currently, this means the fields `opcode`, `target`, `timing` and `resist_dispel`.

note(s):
* this function returns a *new* array, the argument array is not touched.