# Encoders.

Library of encoder converters from a human-readable format into binary more proper ready for writing. To avoid writing out garbage as much as possible, encoders sanitiza their input as much as possible. They also a uniform signature to be used in generic code.

file(s):

* [Source code](../../../internal/encoders.tpa)

Other encoders are available in other modules. This is necessary to avoid circular imports.

note(s):
* all encoders in this file have action and patch variants.

# A. Generic.

`encode_identity STR_VAR value RET return`

The trivial encoder, returning `value` unchanged.

# B. Numeric.

`encode_percentage STR_VAR value RET return`

`encode_positive STR_VAR value RET return`

# C. Text.

`encode_tra_ref STR_VAR value RET return`

Resolves the tra reference `value`, adding its text to the .tlk and returning the corresponding numeric reference.

# D. Opcodes.

`encode_opcode_type STR_VAR value RET return`

`encode_opcode_target STR_VAR value RET return`

`encode_opcode_timing STR_VAR value RET return`

`encode_opcode_resist_dispel STR_VAR value RET return`

`encode_save_bonus STR_VAR value RET return`

# E. Projectiles.

`encode_missile_res STR_VAR value RET return`

Encoder version of `get_missile_res`.

# F. Spells.

`encode_spell_res STR_VAR value RET return`

Encoder version of `get_spell_res`.

`encode_spell_type STR_VAR value RET return`

`encode_school STR_VAR value RET return`

`encode_spell_flags STR_VAR value RET return`

Convert spell flags encoded as a string of binary values to an integer to be written to a spell's main block.

`encode_spell_level STR_VAR value RET return`

# G. Items.

`encode_item_type STR_VAR value RET return`

`encode_item_flags STR_VAR value RET return`

Convert item flags encoded as a string of binary values to an integer to be written to an item's main block.

`encode_proficiency STR_VAR value RET return`
