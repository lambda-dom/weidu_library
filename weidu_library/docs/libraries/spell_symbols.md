# The Spell symbols library.

Library for doing surgery in `spell.ids`.

file(s):

* [Source code](../../spell_symbols.tpa).

## `spell.ids` action functions.

note(s):
* All functions in this section are action functions that patch `spell.ids`.

`add_spell_symbol INT_VAR level STR_VAR name type resource patch = "*"`

A wrapper around the WeiDU `ADD_SPELL` action macro. The function FAIL's if `name` already exists in `spell.ids`, `type` is not a valid spell type to add (see [Add spell types](../../resources/2da/spells/add_types.2da)) or `level` is not an integer in the [0-9] range. `resource` is the spell resource to be copied (full path, no extension) and `patch` is the name of an optional patch function; the function must be in scope and will be called with no arguments.

`add_spell_symbols STR_VAR table patches = "*"`

Add new spell symbols to `spell.ids` using a table that must have the format of [Symbols table](../../resources/2da/templates/add_symbols.2da). `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`; any such patching function will be called with no arguments.
