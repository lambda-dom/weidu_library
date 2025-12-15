# Extended naming spell scheme.

Extended naming scheme for spell to allow referring to them via symbolic names.

file(s):

* [Source code](../../naming.tpa).

# A. Constants.

All tables and arrays below are loaded on `INCLUDE`-ing.

## A. 1. Tables.

`table_namespaces`

The [table](../../resources/2da/naming/namespaces.2da) of namespaces.

# B. Basic functions.

note(s):
* All functions in this section are action functions.

`initialize_namespaces`

This function is idempotent, so it is safe to call it more than oince to guarantee initialization.

`get_spell_namespaces RET path`

Return the (full) `path` of the master namespaces table. FAIL's if the file does not exist.

`load_spell_namespaces RET_ARRAY namespaces`

Load the master namespaces table for reading.

# C. Patching functions.

note(s):
* All functions in this section are patching functions for the master `namespaces` table file.

`add_spell INT_VAR level STR_VAR symbol class`

# D. Searchers.

`get_namespace_spell_resource STR_VAR namespaces symbol RET resource `

Return the spell `resource` associated to `symbol` in the namespaces table, `*` if it does not exist. `namespaces` is the namespaces table loaded with `load_spell_namespaces`. In general it is better to use table references so that the dance to prep and set up table indices is already done -- see the [References module](./references.md).

note(s):
* This function is linear in the size of the table.
