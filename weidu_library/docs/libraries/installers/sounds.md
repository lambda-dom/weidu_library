# The Sounds installer library.

file(s):

* [Source code](../../../installers/sounds.tpa).

# A. Installer.

`install_sounds STR_VAR table resources_dir patches = "*"`

Installer for copying sounds (`.wav` files) with information from `table` (full path) and files located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`. `table` must have the format of [sounds template table](../../../resources/2da/installers/templates/sounds.2da)
