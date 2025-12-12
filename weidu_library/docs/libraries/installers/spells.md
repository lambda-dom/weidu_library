# The Icons installer library.

file(s):

* [Source code](../../../installers/spells.tpa).

# A. Installer.

`install_spells STR_VAR table resources_dir tra = "*" patches = "*"`

Installer for copying tables (`.2da` files) to `destination_dir` (defaulting to `override`) with information from `table` (full path) and files located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table` and `tra` is an optional tra file (full path) to load. `table` must have the format of [Spells template table](../../../resources/2da/installers/templates/spells.2da)
