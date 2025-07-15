# The HLA's library.

A library to patch HLA tables.

file(s):

* [Source code](../../hlas.tpa).

# A. Elementary functions.

note(s):
* all functions have action and patch versions.

The functions in this section manipulate the table `luabbr.2da`.

`get_hla_table STR_VAR kit RET table`

Returns the HLA `table` file (no extension) for the `kit`. If `kit` not listed in the relevant table file (`luabbr.2da`), then it returns `*`.

note(s):
* Technically, this function only returns the first instance of the kit's HLA table; but if there are two instances, then the table is malformed.

`set_hla_table STR_VAR kit table`

Sets the HLA `table` for the `kit`. If the kit is not listed in the relevant table file (`luabbr.2da`), then function FAIL's.

note(s):
* the use case for this function is to set up a kit HLA table file different than the parent's class -- see `replace_table`.

`replace_table STR_VAR kit original new`

# B. HLA table manipulation.

All functions in this section are patch functions for HLA table files.

```weidu
set_hla_attributes INT_VAR
    min_level = 0 - 1
    max_level = 0 - 1
    num_allowed = 0 - 1
STR_VAR
    hla
    icon = "*"
    strref = "*"
    prerequisite = "*"
    excluded = "*"
    alignment = "*"
```

Sets the various fields in the hla row. Note that `hla`, `prerequisite` and `excluded` have the form: prefix, underscore, resource name. Both `prerequisite` and `excluded`, if not null, must already be present as HLA entries in the table or else the function PATCH_FAIL's.

```weidu
add_hla INT_VAR
    min_lev = 1
    max_level = 99
    num_allowed = 1
STR_VAR
    hla
    prefix
    strref = "*"
    icon = "*"
    prerequisite = "*"
    exclusion = "*"
    alignment = "*"
```

Adds an `hla` to the HLA table file. If `hla` is already present, the function PATCH_FAIL's. If the hla resource `hla` does not exist in-game, the function PATCH_FAIL's. Note that `hla`, `prerequisite` and `excluded` have the form: prefix, underscore, resource name.

`delete_hla STR_VAR hla`

Deletes an `hla` from the hla table file. If the `hla` to delete is not in the table, the function PATCH_FAIL's. If `hla` is a pre-requisite of some other hla, the function PATCH_FAIL's. Note that `hla` must have the form: prefix, underscore, resource name.

note(s):
* technically, this function only removes the first instance of the `hla`; but if there are two rows with the same hla, the table is malformed.
* the function does *not* check if the deleted hla is excluded by some other hla, because in most cases the references are circular (e.g. `a` excludes `b` and `b` excludes `a`).

`rename_hla STR_VAR old new`

Rename `old` hla to `new`. Resource `new` must exist in-game, otherwise the function PATCH_FAIL's. Note that both `old` and `new` must have the form: prefix, underscore, resource name.

# C. Helpers.

`deconstruct_ability STR_VAR ability = RET prefix resource`

Desconstruct an ability string into an ability `prefix` and a `resource`. If there is no match, return `*`.

# D. Table installers.

These two functions perform batch HLA deletion and addition from tables.

`delete_hlas STR_VAR table`

`add_hlas STR_VAR table`

`patch_hla_table STR_VAR kit deletions additions`

This is an action function.
