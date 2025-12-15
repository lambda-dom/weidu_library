# Extended naming spell scheme.

Extended naming scheme for spell to allow referring to them via symbolic names.

file(s):

* [Source code](../../naming.tpa).

# A. Constants.

All tables and arrays below are loaded on `INCLUDE`-ing.

## A. 1. Tables.

`path_master_namespaces`

The cached path to the `master_namespaces` table file.

`master_namespaces`

The master [table](../../resources/2da/naming/master_namespaces.2da) of pairs `class => abbreviation`.

note(s):
* The master [table](../../resources/2da/naming/master_namespaces.2da) is indexed but if you make any changes to the table, the indexes will not reflect them. To avoid such a problem put all changes in a component and all readings in another component; this will guarantee the reloading of the table and the synching of the indexes.

# B. Initialization.

note(s):
* All functions in this section have action and patch variants.

`get_master_namespaces RET path`

Return the (full) `path` of the master namespaces table.

`get_extended_namespaces RET path`

Return the (full) `path` of the extended namespaces table.

`initialize_extended_namespaces`

Make sure the two required extended namespace tables exist, and if not, construct them. This function is idempotent, so it is safe to call it more than once.

note(s):
* Usually there is no need to call this function directly as it is as called on module `INCLUDE`-ing.

# C. Loading and reading.

`load_master_namespaces RET_ARRAY namespaces`

Load the master namespaces table for reading.

`load_extended_namespaces RET_ARRAY namespaces`

Load the extended namespaces table for reading.

note(s):
* See the notes above on `master_namespaces` for some footguns that need to be avoided with careful discipline.

# D. Patching functions.

note(s):
* All functions in this section are patching functions for the the relevant table files.

`add_extended_namespace STR_VAR namespace abbreviation`

`add_extended_spell_symbol INT_VAR level STR_VAR symbol namespace patch = "*"`

# E. Searchers.

`get_namespace_spell_resource STR_VAR namespaces symbol RET resource `

Return the spell `resource` associated to `symbol` in the extended namespaces table, `*` if it does not exist. In general, it is better to use table references -- see the [References module](./references.md).

note(s):
* This function is linear in the size of the table. The encoder in the [References module](./references.md) has better asymptotic performance.
