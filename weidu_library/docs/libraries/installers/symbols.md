# The Symbols installer library.

file(s):

* [Source code](../../../installers/symbols.tpa).

# A. Installer.

`install_symbols STR_VAR table patches = "*"`

Add new spell symbols to `spell.ids` using a table that must have the format of the [add spell symbols template table](../../../resources/2da/installers/templates/symbols.2da). `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`; any such patching function will be called with no arguments.

# B. Other installers.

note(s):
* All functions in this section are action functions that patch `spell.ids`.

`alias_spell_symbols STR_VAR table`

Action function that replaces spell symbols in `spell.ids` using a table with the format of [Replace spell symbols table](../../../resources/2da/installers/templates/symbols/alias_symbols.2da).

`change_spell_symbols STR_VAR table`

Change spell symbols in `spell.ids` using a table that must have the format of [Change spell symbols table](../../../resources/2da/installers/templates/symbols/change_symbols.2da).

`replace_spell_symbols STR_VAR table`

Action function that replaces spell symbols in `spell.ids` using a table with the format of [Replace spell symbols table](../../../resources/2da/installers/templates/symbols/replace_symbols.2da).

`deprecate_spell_symbols STR_VAR table`

Action function that deprecates spell symbols in `spell.ids` using a table with the format of [Deprecate spell symbols table](../../../resources/2da/installers/templates/symbols/deprecate_symbols.2da).

`assign_spell_symbol_holes STR_VAR table`

Action function that replaces spell symbol holes in `spell.ids` (unassigned slots) using a table with the format of [Replace spell symbol holes table](../../../resources/2da/installers/templates/symbols/assign_symbol_holes.2da).
