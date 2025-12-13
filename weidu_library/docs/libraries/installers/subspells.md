# The Subspells library.

A library to install copies of standardized subspells.

file(s):

* [Source code](../../../subspells.tpa).

# A. Installers.

note(s):
* All functions in this section are action functions.

`clone_subspells STR_VAR table master_table dir master_tra master_patches patches = "*"`

General installer for subspells via cloning and standardized patching with resource information in `table`.

`install_subspells STR_VAR table patches = "*"`

This is the standard implementation of subspell cloning; a call to `clone_subspells` with arguments:

* dir: dir where subspells to clone can be found, with value `%WEIDU_LIBRARY_DIR%/resources/spl/subspells`

* master_table: the [subspells master table](../../../resources/2da/installers/subspells/subspells.2da)

* master_tra: the [tra file](../../../languages/english/subspells/subspells.tra) containing the generators of spell descriptions.

* master_patches: the [patches file](../../../installers/subspells/patches.tpa) containing the patches referenced by name in the master table.

note(s):
* If you want to provide a name and a description different from the automatically generated one, you must do so in the patch provided in `patches`.
