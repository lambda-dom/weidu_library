# Bits library

A library for doing bit-twiddling.

## A. Basic functions.

note(s):
* all functions in this section are patch functions.

`set_bit INT_VAR offset bit value`

Sets (set or clear) `bit` of byte at `offset` to `value`. Argument `bit` must be in the 0-7 range and `value` in the 0-1 range, otherwise function PATCH_FAIL's.

`set_bits_in_byte INT_VAR offset STR_VAR bits`

Set the `bits` of byte at `offset`. The `bits` values are passed in binary notation, e.g. `LPF set_bits_in_byte INT_VAR offset = offset STR_VAR bits = "01010111" END`. If you need to skip a bit (that is, neither enable nor clear), use `*`, e.g. `LPF set_bits_in_byte INT_VAR offset = offset STR_VAR bits = "01**0111" END`