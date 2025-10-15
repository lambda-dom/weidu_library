# Patchers.

Library of patchers of all kinds.

file(s):

* [Source code](../../patchers.tpa)

# A. Spell patchers.

`add_display_string INT_VAR tra_ref insert_point = 0 - 1`

Add a Display String [139] opcode at `insert_point` (default is appending) to all the headers of a spell. The text to be displayed is the tra reference `tra_ref`. Timing is instant and target is creature (other).

```weidu
patch_resource_reference INT_VAR
    match_opcode
    header = -1
STR_VAR
    match_resource
    resource
    ext = "spl"
    references
```

# B. Creature patchers.

`creature_add_item STR_VAR reference slot flags array`

# C. Script patchers.

`patch_script_spell_replacements STR_VAR replacements`

Patch a script with a `replacements` array of pairs `key => spell` with `spell` spell references. The spell must exist in game, the name must be 7 characters or less and is written upper-cased.

`patch_script_item_replacements STR_VAR replacements`

Patch a script with a `replacements` array of pairs `key => item` with `item` item references. The item must exist in game, otherwise the function FAIL's.

`patch_script_string_replacements STR_VAR replacements tra`

Patch a script with a `replacements` array of pairs `key => tra_ref` with `tra_ref` tra references looked up in the `tra` file (full path, no extension), which is loaded on entering the function and then automatically unloaded on exiting it.
