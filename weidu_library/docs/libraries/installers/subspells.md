# The Subspells library.

A library to install copies of standardized subspells.

file(s):

* [Source code](../../../subspells.tpa).

# A. Installers.

note(s):
* All functions in this section are action functions.

`install_subspells STR_VAR table master_table resources_dir master_tra master_patches patches = "*"`

Installer for subspells via copying and standardized patching with resource information in `table`.

`clone_subspells STR_VAR table patches = "*"`

This is the standard implementation of subspell cloning; a call to `install_subspells` with arguments:

* resources_dir: dir where subspells to clone can be found, with value `%WEIDU_LIBRARY_DIR%/resources/spl/subspells`

* master_table: the [subspells master table](../../../resources/2da/installers/subspells/subspells.2da)

* master_tra: the [tra file](../../../languages/english/subspells/subspells.tra) containing the generators of spell descriptions.

* master_patches: the [patches file](../../../installers/subspells/patches.tpa) containing the patches referenced by name in the master table.
