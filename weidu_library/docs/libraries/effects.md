# The Effects library

A library to handle extended effect .eff files.

file(s):

* [Source code](../../effects.tpa).

# A. Basic functions.

`get_effect_size RET size`

Return the `size` of an opcode in bytes.

# B. Constants.

## B. 1. Tables.

All tables are loaded on `INCLUDE`-ing.

`table_eff_offsets`

[Table](../../resources/2da/effects/offsets.2da) of extended effect offsets. The field names are the same as in WeiDU macros like `ADD_EFFECT`.

# C. Readers and writers.

Specializations of the generic reader and writer for effects.

`get_effect_field STR_VAR field RET value`

`set_effect_field STR_VAR field value`
