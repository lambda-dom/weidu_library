# The Patching library.

A higher-level library to patch-in opcodes into resources.

note(s):

    * library should still be considered experimental.

## A. Functions.

note(s):
* all functions in this section are patch functions.

`patch_opcode_block INT_VAR global = 0 verbose = 1 STR_VAR table dir = "*"`

Patch-in (a spell, an item or a cre) a block of opcodes as described in the 2da file `table` (no extension) using WeiDU's `CLONE_EFFECT` to patch them in and `DELETE_EFFECT` to avoid duplicates.