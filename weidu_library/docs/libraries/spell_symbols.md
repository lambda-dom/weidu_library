# The Spell symbols library.

Library for doing surgery in `spell.ids`.

file(s):

* [Source code](../../spell_symbols.tpa).

# A. `spell.ids` action functions.

note(s):
* All functions in this section are action functions that patch `spell.ids`.

`add_spell_symbol INT_VAR level STR_VAR name type resource patch = "*"`

A wrapper around the WeiDU `ADD_SPELL` action macro. The function FAIL's if `name` already exists in `spell.ids`, `type` is not a valid spell type to add (see [Add spell types](../../resources/2da/spells/add_types.2da)) or `level` is not an integer in the [0-9] range. `resource` is the spell resource to be copied (full path, no extension) and `patch` is the name of an optional patch function; the function must be in scope and will be called with no arguments.

`change_spell_symbol INT_VAR level STR_VAR name type`

Changes the spell symbol `name` to `type` and `level`. This is implemented as a call to `ADD_SPELL` where `name` must already exist in `spell.ids`, so it adds a new slot to `spell.ids` unless `type` and `level` are the same (in which case the call is a no-op). The original spell resource is untouched.

## A. 1. Table interface.

`add_spell_symbols STR_VAR table patches = "*"`

Add new spell symbols to `spell.ids` using a table that must have the format of [Add spell symbols table](../../resources/2da/templates/add_symbols.2da). `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`; any such patching function will be called with no arguments.

`change_spell_symbols STR_VAR table`

Change spell symbols in `spell.ids` using a table that must have the format of [Change spell symbols table](../../resources/2da/templates/change_symbols.2da).

# B. `spell.ids` patchers.

note(s):
* Unless explicitly said otherwise, all functions in this section are patching functions for `spell.ids`.

`replace_spell_symbol STR_VAR new old`

Replaces spell symbol `old` with `new`. The function FAIL's if either `old` is not present in `spell.ids` or `new` is. The underlying spell resource is left untouched.

note(s):
* this function makes the `old` spell symbol unavailable so any code that relies on its existence will fail.

## B. 1. Table interface.

`replace_spell_symbols STR_VAR table`

Action function that replaces spell symbols in `spell.ids` using a table with the format of [Replace spell symbols table](../../resources/2da/templates/replace_symbols.2da).
