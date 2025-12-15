# The Opcodes library.

High-level library to handle the processing of opcodes as arrays.

file(s):

* [Source code](../../opcode_arrays.tpa).

# A. Basic functions.

note(s):
* all functions in this section are patching functions.

`get_opcode_array INT_VAR offset RET_ARRAY array`

Get opcode `array` at `offset`.

`set_opcode_array INT_VAR offset STR_VAR array`

Set all the fields of an opcode at `offset` using the opcode `array`.

# B. Constructing values.

note(s):
* functions in this section have both patch and action versions.

`get_zero_opcode RET_ARRAY array`

Return the opcode `array` with all fields zeroed-out out, except `target` set to `projectile` and `probability1` set to `100`.

`get_equipped_zero_opcode RET_ARRAY array`

Return the zeroed-out opcode `array` with timing mode equipped and target `self`.
