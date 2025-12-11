# The Effect installers library.

file(s):

* [Source code](../../../installers/effects.tpa).

# A. Installers.

`copy_effects STR_VAR table resources_dir patches = "*"`

Installer for copying effects (`.eff` files) with information from `table` (full path) and files located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`. `table` must have the format of [Copy effects template table](../../../resources/2da/installers/templates/copy_effects.2da)

`create_effects STR_VAR table tra = "*" patches = "*"`

Table installer for creating effect `.eff` with the `CREATE_EFFECT` macro and information read from `table` (full path). `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table` and `tra` is an optional tra file (full path) to load. `table` must have the format of [Copy effects template table](../../../resources/2da/installers/templates/create_effects.2da)
