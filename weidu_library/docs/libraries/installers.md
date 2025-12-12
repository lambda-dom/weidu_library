# The Installers library.

A suite of libraries to streamline the installation of game resources.

file(s):

* [Source code](../../installers.tpa).

# A. Anatomy of an installer library.

# B. Available installers.

* [Creatures](./installers/creatures.md): installer for creature `.cre` files.
* [Dialogs](./installers/dialogs.md): compile dialog `.d` files.
* [Effects](./installers/effects.md): installers for effect `.eff` files.
* [Icons](./installers/icons.md): installer for icon `.bam` files.
* [Projectiles](./installers/projectiles.md): installers for projectile `.pro` files.
* [Scripts](./installers/scripts.md): compile script `.baf` files.
* [Sounds](./installers/sounds.md): installer for sounds (`.wav` files).
* [Tables](./installers/tables.md): installer for table `.2da` files.
* [Vvcs](./installers/vvcs.md): installer for animation `.vvc` files.

# C. Managing references.

`load_table_references STR_VAR table RET_ARRAY references`

Construct the arrays of pairs `name => value` from `table` (full path), with name from the first column and value from the last, interpreting these values as table references.

`get_table_reference STR_VAR value array ext RET return`

Gets and validates the resource reference `return` associated to the symbolic name `value` in the `array`, an array loaded with `load_table_references`.
