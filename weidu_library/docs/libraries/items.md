# The Items library.

Library for handling items.

file(s):

* [Source code](../../items.tpa).

# A. Constants.

## A. 1. Tables.

`table_itm_offsets`

[Table](../../resources/2da/items/offsets.2da) of item offsets.

`table_itm_header_offsets`

[Table](../../resources/2da/items/header_offsets.2da) of item header offsets. The field names are the same as in WeiDU macros like `ALTER_SPELL_HEADER`.

## A. 2. Arrays.

`item_flags`

[Array](../../resources/2da/items/flags.2da) with keys the names for item flags and values the associated bit index for the flags word.

`item_header_locations`

[Array](../../resources/2da/items/header_types.2da) of item header types.

`item_header_locations`

[Array](../../resources/2da/items/header_locations.2da) of possible item header locations.

# B. Basic functions.

`get_item_size RET size`

Size in bytes of the main item block.

`get_item_header_size RET size`

Size in bytes of an item header.

# C. Item functions.

note(s):
* all functions in these sections are patch functions.

## C. 1. Main header.

Basic read functions that return the values of fields that should not be read directly.

`get_item_header_count RET count`

Return `count` of headers in the item.

`get_item_headers_offset RET offset`

Return `offset` of the headers block.

`get_item_opcodes_offset RET offset`

Return `offset` of the opcodes block.

`get_equipped_opcode_count RET count`

Return `count` of equipped opcodes in the item.

## C. 2. Equipped opcode functions.

`get_equipped_opcode_offset INT_VAR index RET offset`

Return `offset` of `index` equipped, or global, opcode. If index out of bounds, return -1.

## C. 3. Item header functions.

`get_item_header_offset INT_VAR header RET offset`

Return `offset` of `header` (0-indexed). If `header` out of bounds, return -1.

### C. 3. 1. Item header mutators.

`insert_item_header INT_VAR index`

`append_item_header`

## C. 3. Item header opcode functions.

`get_item_header_opcode_count INT_VAR header RET count`

Return the `count` of opcodes of `header`. If `header` out of bounds, return -1.

`get_item_header_opcode_block_offset INT_VAR header RET offset`

Return `offset` of the opcode block for the `header` (equivalently, the offset of the zeroth header opcode). If `header` is out of bounds, return -1.

`get_item_header_opcode_offset INT_VAR header index RET offset`

Return `offset` of `index` opcode of `header`. If any of `index` or `header` are out of bounds, it returns -1.

# D. Readers and writers.

Specializations of the generic reader and writer for items.

`get_item_field STR_VAR field RET value`

`set_item_field STR_VAR field value`

`get_item_header_field INT_VAR header STR_VAR field RET value`

`set_item_header_field INT_VAR header STR_VAR field value`

## D. 1. Mutators.

`insert_item_equipped_opcode INT_VAR index`

Insert a blank equipped opcode (only non-zero field is probability1 that is set to 100) at `index`. Function FAIL's if `index` out of bounds.

note(s):
* use index `-1` if you want to insert at the end, or append, or use the `append_item_casting_opcode` function.

`append_item_equipped_opcode`

Append a blank equipped opcode (only non-zero field is probability1 that is set to 100).

`insert_item_header_opcode INT_VAR header index`

Insert a blank opcode (only non-zero field is probability1 that is set to 100) at `index` of `header`. Function FAIL's if either `header` or `index` out of bounds.

note(s):
* use index `-1` if you want to insert at the end, or append, or use the `append_item_header_opcode` function.

`append_item_header_opcode INT_VAR header`

Append a blank opcode (only non-zero field is probability1 that is set to 100) to `header`. Function FAIL's if `header` out of bounds.

### D. 1. 1. Block versions.

`insert_item_equipped_block INT_VAR index amount = 1`

Insert a contiguous block of `amount` blank equipped opcodes (only non-zero field is probability1 that is set to 100) at `index`. Function FAIL's if `index` out of bounds.

note(s):
* use index `-1` if you want to insert at the end, or append, or use the `append_item_casting_block` function.

`append_item_equipped_block INT_VAR amount = 1`

Append a contiguous block of `amount` blank equipped opcodes (only non-zero field is probability1 that is set to 100).

`insert_item_header_block INT_VAR header index amount = 1`

Insert a contiguous block of `amount` blank opcodes (only non-zero field is probability1 that is set to 100) at `index` of `header`. Function FAIL's if either `header` or `index` out of bounds.

note(s):
* use index `-1` if you want to insert at the end, or append, or use the `append_item_header_block` function.

`append_item_header_opcode INT_VAR header amount = 1`

Append a contiguous block of `amount` blank opcodes (only non-zero field is probability1 that is set to 100) to `header`. Function FAIL's if `header` out of bounds.

# E. Getters.

`get_item_category_id STR_VAR category RET id`

Get the numeric id of an item type or category as existing in `itemcat.ids`.

`get_item_proficiency_id STR_VAR proficiency RET id`

note(s):
* The names in `wprof.ids` are prefixed by `PROFICIENCY`; this is taken into account, so strip from the passed `proficiency`.
* `none` is alliased to `0`.

# F. Patching `itemexcl.2da`.

note(s):
* all functions in this section are patch functions for `itemexcl.2da`.

`set_item_exclusion INT_VAR exclusion = 1 STR_VAR item`

Sets the `item` (item resource reference, no extension) exclusion flag in the `itemexcl.2da` table. Function FAIL's if `item` does not exist in-game.

# G. Patching `tooltip.2da`.

note(s):
* all functions in this section are patch functions for `tooltip.2da`.

`set_ability_tooltip INT_VAR ability1 = -1 ability2 = -1 ability3 = -1 STR_VAR item`

Sets the tooltips of `item`. The integer arguments are tra references. The function PATCH_FAIL's if `item` does not exist in-game.

note(s):
* this function has the side-effect of (potentially) adding text to the tlk file.
