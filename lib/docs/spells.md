# The Spells library

Library for handling spells.

## A. Constants.

`spell_size`

Size in bytes of the (main) spell block.

`spell_header_size`

Size in bytes of a spell header.

### A. 1. Array constants.

`spell_offsets`

Array of spell offsets.

`spell_header_offsets`

Array of spell header offsets. The field names are the same as in WeiDU macros like ALTER_SPELL_HEADER.

`spell_types`

Array with keys the symbolic names for spell types and values the associated integer values.

## B. Basic functions.

### B. 1. Elementary functions.

note(s):
* all functions in this section are patch functions.

Basic read functions that return the values of fields that are not to be read directly.

`get_spell_header_count RET count`

Return number of spell headers in spell.

`get_spell_headers_offset RET offset`

Return offset of the spell headers block.

`get_spell_opcodes_offset RET offset`

Return offset of the spell opcodes block.

`get_casting_opcode_count RET count`

Return number of casting opcodes in spell.

### B. 2. Read-write functions.

note(s):
* all functions in this section are patch functions.

`get_spell_field STR_VAR field RET value`

Generic read function. Return the value of spell field. If field is not a spell field, or is an internal field like the headers count, function PATCH_FAIL's.

`set_spell_field STR_VAR field value`

Generic write function. Write value, passed as a string, to spell field. If field is not a spell field, or is an internal field like the headers count, function PATCH_FAIL's.

note(s):
* pay attention to the types of the fields, so as not to pass the wrong argument and get a clobbered file. These can be checked in the [spell_offsets.2da](../resources/2da/spell_offsets.2da) table.

#### B. 2. 1. Spell field utilities.

note(s):
* all functions in this section have patch and action versions coded via `DEFINE_DIMORPHIC_FUNCTION`.

`get_spell_type STR_VAR type RET value`

Return the integer `value` corresponding to the symbolic name of spells's `type`. The function returns -1 if `type` is not valid.

note(s):
* the symbolic names can be found in the [spell_types.2da table](../resources/2da/spell_types.2da).

### B. 3. Spell header functions.

note(s):
* all functions in this section are patch functions.

Basic read-write functions for spell headers.

`get_spell_header_offset INT_VAR header = 0 RET offset`

Return offset of (0-indexed) header. If header out of bounds return -1.

`get_spell_header_field INT_VAR header = 0 STR_VAR field RET value`

Generic read function. Read the value of a spell header field. PATCH_FAIL's if header out of bounds or field is not a spell head field or is an internal, private field.

`set_spell_header_field INT_VAR header = 0 STR_VAR field value`

Generic write function. Write value, passed as a string, to spell header field. If field is not a spell header field, or is an internal field like the header opcode count, function PATCH_FAIL's.

note(s):
* pay attention to the types of the fields, so as not to pass the wrong argument and get a clobbered file. These can be checked in the [spell_header_offsets.2da](../resources/2da/spell_header_offsets.2da) table.

`match_spell_header_against_array INT_VAR header = 0 STR_VAR array RET bool`

Matches spell `header` field by field against the associative `array`. Function PATCH_FAIL's if `header` out of bounds or any of the array fields is not a spell header field.

note(s):
* arguments stuffed in array to simplify the function's signature.

### B. 4. Casting opcode functions.

note(s):
* all functions in this section are patch functions.

`get_casting_opcode_offset INT_VAR index = 0 RET offset`

Return offset of index casting (global) opcode. If index out of bounds, return -1.

`get_casting_opcodes_array RET_ARRAY offsets`

Return the array of casting opcode offsets. Returns the empty array if spell has no casting opcodes. This is useful if you want to apply a function to every opcode like `set_opcode_field` from the [opcodes library](./opcodes.md). The general template is:

```weidu
LPF get_casting_opcodes_array RET_ARRAY offsets END
PHP_EACH offsets AS index => offset BEGIN
    LPF set_opcode_field INT_VAR offset = offset ...
END
```

note(s):
* be *very* careful if adding or removing opcodes with this pattern, as it is *very easy* to get the bounds wrong and invalidate the file -- in other words, as a general advice, unless you know exactly what you are doing do *not* add or remove opcodes while looping through the sequence of casting opcodes.

### B. 5. Spell header opcode functions.

`get_spell_header_opcode_count INT_VAR header = 0 RET count`

Return the number of opcodes of header. If header is out of bounds, return -1.

`get_spell_header_opcode_block_offset INT_VAR header = 0 RET offset`

Return offset of the opcode block for the header. If header is out of bounds, return -1.

`get_spell_header_opcode_offset INT_VAR header = 0 index = 0 RET offset`

Return offset of index opcode of header. If any of index or header are out of bounds, it returns -1.

`get_spell_header_opcodes_array INT_VAR header = 0 RET_ARRAY offsets`

Return the array of the header's opcode offsets. Returns the empty array if header has no casting opcodes. The function PATCH_FAIL's if `header` out of bounds.

note(s):
* same advice as `get_casting_opcodes_array`.

## C. Utilities.

Miscellaneous utilities.

### C. 1. Readers.

note(s):
* unless explicitly mentioned otherwise all functions in this section have both action and patch versions (coded via `DEFINE_DIMORPHIC_FUNCTION`).

`get_spell_res STR_VAR spell RET resource`

Return resource associated to (symbolic) name of `spell`. Return `*` if `spell` not in spell.ids.

`get_school STR_VAR school RET id`

Return the magical school row index, -1 if `school` is not in `mschool.2da`.

`get_sectype STR_VAR sectype RET id`

Return the sectype row index, -1 if `sectype` is not in `msectype.2da`.

`get_splprot_row STR_VAR name RET id`

Return the (first) row index in `splprot.2da` with matching `name`, which is the row name minus leading decimal characters. Returns -1 if no matching row is found.
