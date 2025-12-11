# The Animations installer library.

file(s):

* [Source code](../../../installers/vvcs.tpa).

# A. Installer.

`install_vvcs STR_VAR table resources_dir patches = "*"`

Installer for copying animations (`.vvc` files) with information from `table` (full path) and files located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`. `table` must have the format of [Animations template table](../../../resources/2da/installers/templates/vvcs.2da)
