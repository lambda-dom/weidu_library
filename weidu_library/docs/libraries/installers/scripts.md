# The Scripts installer library.

file(s):

* [Source code](../../../installers/scripts.tpa).

# A. Installers.

`install_scripts STR_VAR table resources_dir tra = "*" patches = "*"`

Installer for compiling scripts (`.baf` files) into `.bcs` files with information from `table` (full path) and files located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table` and `tra` is an optional tra file (full path) to load. `table` must have the format of [Scripts template table](../../../resources/2da/installers/templates/scripts.2da)
