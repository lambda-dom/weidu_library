Utilities to patch-in lists of opcodes as a single block (e.g. immunity to, say, charm or blindness).

file(s):

* [Source code](../../blocks.tpa)

## A. Functions.

```weidu
patch_block_with_table INT_VAR
    match_opcode
    globals = 0
    header = -1
STR_VAR
    table
    match_resource = "*"
```

Patch in a block of opcodes from `table` using `match_opcode` as a match for the anchor and extra fields (saves, dispel, etc.). `table` is the full path to a .2da table in the format of [Template Block Table](../../resources/2da/blocks/templates/blocks.2da) containing the info on the opcodes to add.

`append_item_block_with_table STR_VAR table`

Append a block of opcodes from `table` as equipped opcodes in an item. `table` is the full path to a .2da table in the format of [Template Block Table](../../resources/2da/blocks/templates/blocks.2da) containing the info on the opcodes to add.

```weidu
patch_block INT_VAR
    match_opcode
    globals = 0
    header = -1
STR_VAR
    block
    match_resource = "*"
```

A call to `patch_block_with_table` using the pre-defined blocks in the `resources/2da/blocks` dir. More specifically, it is just the call:

```weidu
LPF patch_block_with_table INT_VAR
    match_opcode = match_opcode
    globals = globals
    header = header
STR_VAR
    table = "%WEIDU_LIBRARY_DIR%/resources/2da/blocks/%block%.2da"
    match_resource = "%match_resource%"
END
```

`append_item_block STR_VAR block`

A call to `append_item_block_with_table` using the pre-defined blocks in the `resources/2da/blocks` dir. More specifically, it is just the call:

```weidu
LPF append_item_block_with_table STR_VAR
    table = "%WEIDU_LIBRARY_DIR%/resources/2da/blocks/%block%.2da"
END
```
