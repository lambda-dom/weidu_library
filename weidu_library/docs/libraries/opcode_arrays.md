# The Opcodes library.

High-level library to handle the processing of opcodes as arrays.

file(s):

* [Source code](../../opcode_arrays.tpa).

# A. Basic functions.

`get_opcode_array INT_VAR offset RET_ARRAY array`

Get opcode `array` at `offset`.

`set_opcode_array INT_VAR offset STR_VAR array`

Set all the fields of an opcode at `offset` using the opcode `array`.

# B. Constructing values.

`get_zero_opcode RET_ARRAY array`

Return the opcode `array` with all fields zero-out out, except `target` (set to `projectile`) and `probability1` set to `100`.

note(s):
* this is both a patch and action function.

`get_equipped_zero_opcode RET_ARRAY array`

Return the opcode `array` zero-out with timing mode equipped and target self.
