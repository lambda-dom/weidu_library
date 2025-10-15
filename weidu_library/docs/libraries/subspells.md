# The Subspells library.

A library to install copies of standardized subspells.

file(s):

* [Source code](../../subspells.tpa).

# A. Installers.

note(s):
* All functions in this section are action functions.

`install_subspells STR_VAR table subspells dir tra patches`

Installer for subspells via copying and standardized patching with resource information in `table`.

`install_subspells_library STR_VAR table`

This is the standard implementation of subspell cloning; a call to `install_subspells` with arguments:

* subspells: the [subspells table](../../resources/2da/subspells/subspells.2da)

* dir: dir where subspells to clone can be found, with value `WEIDU_LIBRARY_DIR/resources/spl/subspells`

* tra: the [tra file](../../languages/english/subspells/subspells.tra) containing the generators of spell descriptions.

* patches: the [patches file](../../internal/installers/subspells/patches.tpa) containing the patches referenced by name in the [subspells table](../../resources/2da/subspells/subspells.2da).
