# The Projectile installers library.

file(s):

* [Source code](../../../installers/projectiles.tpa).

# A. Installer.

`copy_projectiles STR_VAR table resources_dir patches = "*"`

Installer for copying projectiles (`.pro` files) with information from `table` (full path) and files located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`. `table` must have the format of [Copy projectiles template table](../../../resources/2da/installers/templates/copy_projectiles.2da)

`add_projectiles STR_VAR table resources_dir patches = "*"`

Installer for adding `.pro` files with information from `table` (full path) and files located in `resources_dir`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`. `table` must have the format of [Add projectiles template table](../../../resources/2da/installers/templates/add_projectiles.2da)
