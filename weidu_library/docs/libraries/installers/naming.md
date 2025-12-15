# The Symbols installer library.

file(s):

* [Source code](../../../installers/naming.tpa).

# A. Installers.

`install_extended_symbols STR_VAR table patches = "*"`

Add new symbols to the extended namespace table using a table that must have the format of the [add spell symbols template table](../../../resources/2da/installers/templates/symbols.2da). `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`; any such patching function must have the signature `STR_VAR destination`.
