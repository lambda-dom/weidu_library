# The Dialogs installer library.

file(s):

* [Source code](../../../installers/dialogs.tpa).

# A. Installers.

`install_dialogs STR_VAR table resources_dir tra = "*" patches = "*"`

Installer for compiling dialogs (`.d` files) with information from `table` (full path) and resources located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table` and `tra` is an optional tra file (full path) to load. `table` must have the format of [Dialogs template table](../../../resources/2da/installers/templates/dialogs.2da)
