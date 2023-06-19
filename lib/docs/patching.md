# The Patching library.

A higher-level library to patch-in opcodes into resources.

## A. Functions.

note(s):
* all functions in this section are patch functions.

`patch_opcode_block INT_VAR global = 0 STR_VAR table`

Patch-in (a spell, an item or a cre) a block of opcodes as descriobed in the 2da file `table` (no extension) using WeiDU's `DELETE_EFFECT` to avoid duplicates and `CLONE_EFFECT`.