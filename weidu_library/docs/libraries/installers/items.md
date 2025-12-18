# The Icons installer library.

file(s):

* [Source code](../../../installers/items.tpa).

# A. Installer.

`install_items STR_VAR table dir tra = "*" patches = "*"`

Installer for copying items (`.itm` files) with information from `table` (full path) and located in `dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table` and `tra` is an optional tra file (full path) to load. `table` must have the format of [Items template table](../../../resources/2da/installers/templates/items.2da)

# B. Other installers.

`install_item_tooltips STR_VAR table references tra = "*"`

`install_item_exclusion STR_VAR table references`
