# Extended naming spell scheme.

Extended naming scheme for spell to allow referring to them via symbolic names.

file(s):

* [Source code](../../naming.tpa).

# A. Constants.

All tables and arrays below are loaded on `INCLUDE`-ing.

## A. 1. Tables.

`master_namespaces`

The master [table](../../resources/2da/naming/master_namespaces.2da) of pairs `class => abbreviation`.

note(s):
* The master [table](../../resources/2da/naming/master_namespaces.2da) is *not* copied into `override` so adding new namespaces or changing abbreviations is not possible without changing the weidu_library source. This is such, at least for the time being, to avoid bootstrapping issues.

# B. Basic functions.

note(s):
* All functions in this section are action functions.

`get_namespaces_resource RET resource`

Return the in-game `resource` of the master namespaces table (no extension).

`initialize_namespaces`

Make sure the master namespaces table exist, and if not, initialize it. This function is idempotent, so it is safe to call it more than once.

note(s):
* Currently this table is called `extended_namespaces.2da` and is assumed that no other mod is using such a resource (otherwise you will get errors).

`load_spell_namespaces RET_ARRAY namespaces`

Load the master namespaces table for reading.

# C. Patching functions.

note(s):
* All functions in this section are patching functions for the master `namespaces` table file.

`add_extended_spell_symbol INT_VAR level STR_VAR symbol class patch = "*"`

# D. Searchers.

`get_namespace_spell_resource STR_VAR namespaces symbol RET resource `

Return the spell `resource` associated to `symbol` in the namespaces table, `*` if it does not exist. `namespaces` is the namespaces table loaded with `load_spell_namespaces`. In general, it is better to use table references -- see the [References module](./references.md).

note(s):
* This function is linear in the size of the table. The encoder in the [References module](./references.md) has better asymptotic performance.
