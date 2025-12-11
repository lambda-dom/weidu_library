# The Installers library.

A suite of libraries to streamline the installation of game resources.

file(s):

* [Source code](../../installers.tpa).

# A. Anatomy of an installer library.

# B. Managing references.

`load_table_references STR_VAR table RET_ARRAY references`

Construct the arrays of pairs `name => value` from `table` (full path), with name from the first column and value from the last, interpreting these values as table references.

`get_table_reference STR_VAR value array ext RET return`

Gets and validates the resource reference `return` associated to the symbolic name `value` in the `array`, an array loaded via `load_table_references`.
