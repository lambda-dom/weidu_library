# The Installers library.

A suite of libraries to streamline the installation of game resources.

file(s):

* [Source code](../../installers.tpa).

# A. Anatomy of an installer library.

An installer for resources of a given type has, up to some details, the general form:

`install_resources STR_VAR table resources_dir patches = "*" tra = "*"`

Installer for resources of a given type with resource information in `table`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table` and `tra` is an optional tra file and `resources_dir` is the directory wehere the resources are located.

For each type of resource there is a template example for the structure of the .2da table located in `%WEIDU_LIBRARY_DIR%/resources/2da/installers/templates`. All these tables share the first and the last fields, with a (mostly) common meaning to them: `resource` is a symbolic name for the resource to be installed, usually just the file basename. `install` is a flag to selectively enable or disable installing for debugging purposes. `patch` is a resource patcher, a function with signature `STR_VAR destination = "*"` that *must* be in scope, and `destination` is a (computed) resource reference that will serve as the destination file basename. These patchers can be brought into scope by passing the appropriate file in the `patches` argument of the installer. Finally, `override` is a debugging flag that controls what to do if a same-named resource already exists: if `0` then overriding is not allowed and if the resource already the function FAIL's, if `1` overriding is allowed. On the other hand if the `override` is `2` then the overriden resource *must* already exist otherwise the function FAIL's.

# B. Available installers.

* [Blocks](./installers/blocks.md): patch in standardized blocks of opcodes.
* [Creatures](./installers/creatures.md): installer for creature `.cre` files.
* [Dialogs](./installers/dialogs.md): compile dialog `.d` files.
* [Effects](./installers/effects.md): installers for effect `.eff` files.
* [Icons](./installers/icons.md): installer for icon `.bam` files.
* [Items](./installers/items.md): installer for `.itm` items.
* [Naming](./installers/naming.md): installer for spell symbols in the extended namespace.
* [Projectiles](./installers/projectiles.md): installers for projectile `.pro` files.
* [Scripts](./installers/scripts.md): compile script `.baf` files.
* [Sectypes](./installers/sectypes.md): installer for new sectypes.
* [Sounds](./installers/sounds.md): installer for sounds (`.wav` files).
* [Spells](./installers/spells.md): installer for `.spl` spells.
* [Subpells](./installers/subspells.md): installer for subspells via cloning.
* [Symbols](./installers/symbols.md): various installers for doing surgery in `spell.ids`.
* [Tables](./installers/tables.md): installer for table `.2da` files.
* [Vvcs](./installers/vvcs.md): installer for animation `.vvc` files.

# C. Managing references.

`load_table_references STR_VAR table RET_ARRAY references`

Construct the arrays of pairs `name => value` from `table` (full path), with name from the first column and value from the last, interpreting these values as table references.

`get_table_reference STR_VAR value array ext RET return`

Gets and validates the resource reference `return` associated to the symbolic name `value` in the `array`, an array loaded with `load_table_references`.
