# The Blocks installer library.

file(s):

* [Source code](../../../installers/blocks.tpa).

# A. Primitives.

## A. 1. Items.

Unless explicitly said otherwise, all functions in this section are item patching functions.

`append_item_equipped_block STR_VAR table`

Append the block of opcodes from `table` to an item as equipped opcodes. `table` is the (full) path to a .2da table in the format of [Template Block Table](../../../resources/2da/installers/templates/blocks/equipped.2da) containing the info on the opcodes to add.

`append_item_header_block INT_VAR header STR_VAR table`

Append the block of opcodes from `table` to an item `header`. `table` is the (full) path to a .2da table in the format of [Template Block Table](../../../resources/2da/installers/templates/blocks/full.2da) containing the info on the opcodes to add. Function FAIL's if `header` out of bounds.
