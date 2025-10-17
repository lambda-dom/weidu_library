# The Spells library.

Library for handling spells.

file(s):

* [Source code](../../spells.tpa).

# A. Basic functions.

`get_spell_size RET size`

Size in bytes of the main spell block.

`get_spell_header_size RET size`

Size in bytes of a spell header.

# B. Constants.

All tables and arrays are loaded on `INCLUDE`-ing.

## B. 1. Tables.

`spell_offsets`

[Table](../../resources/2da/spells/offsets.2da) of spell offsets.

`spell_header_offsets`

[Table](../../resources/2da/spells/header_offsets.2da) of spell header offsets. The field names are the same as in WeiDU macros like `ALTER_SPELL_HEADER`.

## B. 2. Arrays.

`spell_types`

[Array](../../resources/2da/spells/types.2da) with keys the symbolic names for spell types and values the associated integer values.

`spell_flags`

[Array](../../resources/2da/spells/flags.2da) with keys the names for spell flags and values the associated bit index for the flags word.

# C. Spell functions.

note(s):
* all functions in these sections are patch functions.

## C. 1. Main header.

Basic read functions that return the values of read-only spell fields.

`get_spell_header_count RET count`

Return `count` of spell headers in spell.

`get_spell_headers_offset RET offset`

Return `offset` of the spell headers block.

`get_spell_opcodes_offset RET offset`

Return `offset` of the spell opcodes block.

`get_casting_opcode_count RET count`

Return `count` of casting, or global, opcodes in spell.

## C. 2. Casting opcode functions.

`get_casting_opcode_offset INT_VAR index RET offset`

Return `offset` of `index` casting, or global, opcode. If `index` out of bounds, return -1.

## C. 3. Spell header functions.

`get_spell_header_offset INT_VAR header RET offset`

Return `offset` of (0-indexed) `header`. If `header` out of bounds, return -1.

## C. 4. Spell header opcode functions.

`get_spell_header_opcode_count INT_VAR header RET count`

Return the `count` of opcodes of `header`. If `header` is out of bounds, return -1.

`get_spell_header_opcode_block_offset INT_VAR header RET offset`

Return `offset` of the opcode block for the `header` (equivalently, the offset of the 0th header opcode). If `header` is out of bounds, return -1.

`get_spell_header_opcode_offset INT_VAR header index RET offset`

Return `offset` of `index` opcode of `header`. If any of `index` or `header` are out of bounds, it returns -1.

## C. 5. Spell header patchers.

Convenience spell header patcher that applies a field change to every header.

`set_spell_header_fields STR_VAR field value`

# D. Readers and writers.

Specializations of the generic reader and writer for spells.

`get_spell_field STR_VAR field RET value`

`set_spell_field STR_VAR field value`

`get_spell_header_field INT_VAR header STR_VAR field RET value`

`set_spell_header_field INT_VAR header STR_VAR field value`

# E. Getters.

`get_spell_res STR_VAR spell RET resource`

Return the `resource` associated to symbolic name of `spell` in `spell.ids`. Function returns `*` if `spell` is not in spell.ids.

`get_spell_type_id STR_VAR type RET id`

Get the type `id` of the spell `type`.

`get_spell_school_id STR_VAR school RET id`

Get the `id` of the magic `school`, -1 if `school` not valid.

note(s):
* In the current implementation, each call to this function requires opening `mschool.2da` and perform a linear search.
