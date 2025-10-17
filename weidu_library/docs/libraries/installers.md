# The Installers library.

A library to streamline the installation of game resources.

file(s):

* [Source code](../../installers.tpa).

# A. Constants.

## A. 1. Tables.

All tables are loaded on `INCLUDE`-ing.

`installers`

The master [table](../../resources/2da/installers/installers.2da) containing all the information needed to install the resources.

# B. Basic functions.

note(s):
* All functions in this section have both patch and action variants.

`get_installer_extension STR_VAR type RET extension`

Return the file extension for resources of `type`.

`get_installer_fields STR_VAR type RET fields`

Return the list of `fields` as a `:`-separated string for the installer table of resources of type `type`.

# C. Installer.

note(s):
* All functions in this section are action functions.

`install_resources STR_VAR type table patches = "*" tra = "*" dir = "*"`

Installer for resources of `type` with resource information in `table`. `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`. Finally, `tra` is an optional tra file and `dir` is an optional directory wehere the resources are located, defaulting to a standard location depending on `type` (e. g. `%MOD_FOLDER%/resources/%ext%`, where `ext` is the resource extension associated to `type`).

For each `type` of resource there is a template example for the structure of the .2da table located in `%WEIDU_LIBRARY_DIR%/resources/2da/installers/templates`. All these tables share the first two and the last three fields, with a (mostly) common meaning to them: `resource` is a symbolic name for the resource to be installed, usually just the file basename. `install` is a flag to selectively enable or disable installing for debugging purposes. `patch` is a resource patcher, a function with signature `STR_VAR destination = "*"` that *must* be in scope, and `destination` is a (computed) resource reference that will serve as the destination file basename. These patchers can be brought into scope by passing the appropriate file in the `patches` argument of `install_resources`. Finally, `override` is a debugging flag that controls what to do if a same-named resource already exists: if `0` then overriding is not allowed and if the resource already the function FAIL's, if `1` overriding is allowed. On the other hand if the `override` is `2` then the overriden resource *must* already exist otherwise the function FAIL's.

## C. 1. `install_resources` calling sequence.

`get_installer_writer STR_VAR type RET writer`

`get_installer_patcher STR_VAR type RET patcher`

`get_installer_handler STR_VAR type RET handler`

# D. Managing references.

`load_table_references STR_VAR tables dir = "*" RET_ARRAY references`

Construct the arrays of pairs `name => value` from each table in the `tables` list, with name from the first column and value from the last and interpreting the values as table references, merging them (left to right). `dir` is the (optional) directory where the tables are located, defaulting to the standardized cxomponent resources dir.

`get_table_reference STR_VAR value array ext RET return`

Gets and validates the resource reference `return` associated to the symbolic name `value` in the `array`, an array loaded via `load_table_references`.

# E. Types of installers.

* table: copy `2da` files.

* icon: copy `bam` files.

* animation: copy `vvc` files.

* sound: copy `wav` files.

* creature: copy `cre` files.

* copy_efect: copy `eff` files.

* create_efect: table interface around `CREATE_EFFECT` to create `eff` files.

* script: copy and compile `baf` files.

* dialog: copy and compile `d` files.

* patch_item: patch in-game `itm` files.

* copy_item: copy `itm` files.

* copy_item_simplified: copy `itm` files, but with a simplified table format. For items like a summon's weapons, that do not need as much information as ordinary PC-usable items.

* add_projectile: table interface around `ADD_PROJECTILE` to install `pro` files.

* copy_projectile: copy `itm` files.

* spell: copy `spl` files.

* subspell: install standardized spells.
