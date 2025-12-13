# The Effect installers library.

file(s):

* [Source code](../../../installers/creatures.tpa).

# A. Installers.

`copy_creatures STR_VAR table resources_dir tra = "*" patches = "*"`

Installer for copying effects (`.eff` files) with information from `table` (full path) and files located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table` and `tra` is an optional tra file (full path) to load. `table` must have the format of [Copy creatures template table](../../../resources/2da/installers/templates/creatures.2da).
