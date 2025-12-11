# The Icons installer library.

file(s):

* [Source code](../../../installers/icons.tpa).

# A. Installer.

`install_icons STR_VAR table resources_dir patches = "*"`

Installer for copying icons (`.bam` files) with information from `table` (full path) and files located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`. `table` must have the format of [icons template table](../../../resources/2da/installers/templates/icons.2da)
