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

Return the file extension of resources of `type`.

`get_installer_fields STR_VAR type RET fields`

Return the list of `fields` as a `:`-separated string for the installer table of resources of type `type`.

# B. 1. Calling sequence.

`get_installer_writer STR_VAR type RET writer`

`get_installer_patcher STR_VAR type RET patcher`

`get_installer_handler STR_VAR type RET handler`

# C. Installer.

note(s):
* All functions in this section are action functions.

`install_resources STR_VAR type table patches = "*" tra = "*" dir = "*"`

Installer for resources of `type` with resource information in `table` (full path). `patches` is an optional file to be `INCLUDED` containing patching functions referenced by name in `table`; any such patching function will be called with no arguments. Finally, `tra` is an optional tra file and `dir` is an optional directory wehere the resources are located, defaulting to a standard location depending on `type` (e. g. `%MOD_FOLDER%/resources/%ext%`, where `ext` is the resource extension associated to `type`).

For each `type` of resource there is a template example for the structure of the .2da table located in `%WEIDU_LIBRARY_DIR%/resources/2da/installers/templates`.

# D. Managing references.

`get_table_references STR_VAR tables dir = "*" RET_ARRAY references`

`get_table_ref STR_VAR value array RET return`
