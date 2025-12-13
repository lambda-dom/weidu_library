# The Symbols installer library.

file(s):

* [Source code](../../../installers/symbols.tpa).

# A. Installer.

`install_symbols STR_VAR table patches = "*"`

Installer for spell symbols with information from `table` (full path). `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`. `table` must have the format of [Spell symbols template table](../../../resources/2da/installers/templates/symbols.2da)
