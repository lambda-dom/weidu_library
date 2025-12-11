# The Icons installer library.

file(s):

* [Source code](../../../installers/tables.tpa).

# A. Installer.

`install_tables STR_VAR table resources_dir destination_dir = "override" tra = "*" patches = "*"`

Installer for copying tables (`.2da` files) to `destination_dir` (defaulting to `override`) with information from `table` (full path) and files located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table` and `tra` is an optional tra file (full path) to load. `table` must have the format of [tables template table](../../../resources/2da/installers/templates/tables.2da)

note(s):
* the override flag is only checked if `destination_dir` is the default `override`.
