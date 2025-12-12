# The Icons installer library.

file(s):

* [Source code](../../../installers/items.tpa).

# A. Installer.

`install_items STR_VAR table resources_dir tra = "*" patches = "*"`

Installer for copying items (`.itm` files) with information from `table` (full path) and located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table` and `tra` is an optional tra file (full path) to load. `table` must have the format of [Items template table](../../../resources/2da/installers/templates/items.2da)
