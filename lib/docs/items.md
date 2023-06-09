# The Items library

A utilities library for handling items.

## A. Constants.

`item_size`

Size in bytes of the (main) item block.

`item_header_size`

Size in bytes of an item header.

### A. 1. Arrays.

`item_offsets`

Array of item offsets. The field names are the same as in WeiDU macros like `ADD_ITEM_EFFECT`.

`item_header_offsets`

Array of item header offsets. The field names are, for the most part, the same as in WeiDU macros like `ALTER_ITEM_HEADER`.

`item_types`

Array with keys the symbolic names for item types and values the associated integer values.

`item_proficiencies`

Array with keys the symbolic names for item proficiencies and values the associated integer values.

note(s):
* only the BG2 proficiencies are in the array.

## B. Item functions.

note(s):
* all functions in this section are patch functions.

### B. 1. Basic functions.

Basic read functions that return the values of fields that should not be read directly.

`get_item_header_count RET count`

Return number of headers in the item.

`get_item_headers_offset RET offset`

Return offset of the headers block.

`get_item_opcodes_offset RET offset`

Return offset of the opcodes block.

`get_equipped_opcode_count RET count`

Return number of equipped opcodes in the item.

### B. 2. Read-write functions.

`get_item_field STR_VAR field RET value`

Generic read function. Return the value of item `field`. If field is not an item field, function PATCH_FAIL's.

note(s):
* casing of `field` is irrelevant.

`set_item_field STR_VAR field value`

Generic write function. Write `value`, passed as a string, to item `field`. If field is not an item field, function PATCH_FAIL's.

note(s):
* casing of `field` is irrelevant.
* pay attention to the types of the fields, so as not to pass the wrong argument and get a clobbered file. These can be checked in the [item_offsets.2da table](../resources/2da/item_offsets.2da).

#### B. 2. 1. Item field utilities.

note(s):
* all functions in this section have patch and action versions coded via `DEFINE_DIMORPHIC_FUNCTION`.

`get_item_type STR_VAR type RET value`

Return the integer `value` corresponding to the symbolic name of item's `type`. The function returns -1 if `type` is not valid.

note(s):
* casing of `type` is irrelevant.
* the symbolic names can be found in the [item_types.2da table](../resources/2da/item_types.2da).

`get_item_proficiency STR_VAR proficiency RET value`

Return the integer `value` corresponding to the symbolic name of item's `proficiency`. The function returns -1 if `proficiency` is not valid.

note(s):
* casing of `proficiency` is irrelevant.
* the symbolic names can be found in the [item_proficiencies.2da table](../resources/2da/item_proficiencies.2da).

### B. 3. Item header functions.

`get_item_header_offset INT_VAR header = 0 RET offset`

Return offset of `header` (0-indexed). If `header` out of bounds, return -1.

`get_item_header_field INT_VAR header = 0 STR_VAR field RET value`

Generic read function. Read the value of an item header `field`.

note(s):
* casing of `field` is irrelevant.

`set_item_header_field INT_VAR header = 0 STR_VAR field value`

Generic write function. Write `value`, passed as a string, to item header `field`. Function PATCH_FAIL's if `header` out of bounds or `field` is not an item header field.

note(s):
* casing of `field` is irrelevant.
* pay attention to the types of the fields, so as not to pass the wrong argument and get a clobbered file. These can be checked in the [item_header_offsets.2da table](../resources/2da/item_header_offsets.2da).

### B. 4. Equipped opcode functions.

`get_equipped_opcode_offset INT_VAR index = 0 RET offset`

Return offset of `index` equipped, or global opcode. If index out of bounds, return -1.

### B. 5. Item header opcode functions.

`get_item_header_opcode_count INT_VAR header = 0 RET count`

Return the number of opcodes of `header`. If `header` out of bounds, return -1.

`get_item_header_opcode_block_offset INT_VAR header = 0 RET offset`

Return offset of the opcode block for the `header`. If `header` is out of bounds, return -1.

`get_item_header_opcode_offset INT_VAR header = 0 index = 0 RET offset`

Return offset of `index` opcode of `header`. If any of `index` or `header` are out of bounds, it returns -1.

## C. Item mutators.

### C. 1. Addition and removal of headers.

The next batch of functions, adds and removes item headers. They should not be needed, but either WeiDU lacks some of such basic functionality or it does not work quite the way we need.

`insert_item_header INT_VAR index = 0`

Inserts a new, blank item header at `index`. Function PATCH_FAIL's if `index` is not in the interval `[-1, count]` where count is the number of existing headers and `-1` means insert at the end (same as `count`).

note(s):
* any other header fields must be set via existing functions such as `ALTER_ITEM_HEADER` or the functions in this library.

### C. 2. Addition and removal of opcodes.

The next batch of functions add and remove opcodes. They should not be needed, but either WeiDU lacks some of such basic functionality or it does not work quite the way we need.

`insert_item_opcode INT_VAR block = 0 index = 0`

Insert a new, blank opcode in `block` at `index`. If `block` is `-1` then it is treated as inserting a global opcode in the equipped opcode block; all other values correspond to (0-index) spell headers, in which case the function PATCH_FAIL's if the condition `0 <= block < count` is not satisfied, with count the number of headers. The function PATCH_FAIL's if `index` is not in the interval `[-1, count]` where count is the number of existing opcodes in the block and `-1` means insert at the end (same as `count`).

note(s):
* all the fields have null value with the exception of `probability1`that is set to `100`. Any other opcode fields must be set via existing functions such as `ALTER_EFFECT` or the functions in this library.

## D. Miscellaneous utilities.

note(s):
* all functions in this section have action and patch versions, coded via `DEFINE_DIMORPHIC_FUNCTION`.

`set_item_exclusion INT_VAR exclusion = 1 STR_VAR item`

Sets the `item` exclusion flag in the `itemexcl.2da` table. Function FAIL's if `item` does not exist in-game.

note(s):
* this function opens `itemexcl.2da`, changes a few entries, pretty-prints, etc. If chaining several calls it can incur a performance penalty.

`set_ability_tooltip INT_VAR tra_ref tlk_ref = 0 ability = 0 STR_VAR item`

Sets the tooltip of item `item` for ability `ability` to (the tlk reference of) the text of `tra_ref`, a tra reference. If `tra_ref` is not passed (or is `0`) then it uses the tlk_ref directly.

Function FAIL's if `item` does not exist in-game.

note(s):
* this function has the side-effect of (potentially) adding text to the tlk file, if it is passed a tra reference.
* this function opens `tooltip.2da`, changes a few entries, pretty-prints, etc. If chaining several calls it can incur a performance penalty.
