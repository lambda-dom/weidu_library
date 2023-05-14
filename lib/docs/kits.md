# The Kits library.

A library for tweaking classes and kits.

## A. Elementary functions.

note(s):
* all functions in this section have action and patch versions, coded via `DEFINE_DIMORPHIC_FUNCTION`.

`get_kit_clab STR_VAR kit RET clab`

Return the kit's clab file. Returns `*` if kit is not present in `kitlist.2da`.

note(s):
* technically, this returns the first `kit` match, but kits are unique in `kitlist.2da`.

## B. Descriptions.

note(s):
* all functions in this section have action and patch versions, coded via `DEFINE_DIMORPHIC_FUNCTION`.

`set_class_description INT_VAR descr STR_VAR class`

Set the description of a class in the .2da file `clastext.2da`. The argument descr is a tra reference. Function FAIL's if kit not found in the relevant table.

note(s):
* this function has the side-effect of (potentially) adding the text of the tra reference to the tlk file.

`set_kit_description INT_VAR descr STR_VAR kit`

Set the new description of a kit in the .2da file `kitlist.2da`. The argument descr is a tra reference. Function FAIL's if kit not found in the relevant table.

note(s):
* this function has the side-effect of (potentially) adding the text of the tra reference to the tlk file.
* in the EE's you usually have to call `set_class_description` for a kit as well. To make matters worse, this does *not* cover all class descriptions used by the engine (some of these are hard-coded and picked up in the ui).

## C. Proficiencies.

All functions in this section are patch functions for the table `weapprof.2da`. The caller is responsible for opening the file, pretty-printing, etc. A typical workflow would be something like:

```weidu
COPY_EXISTING ~weapprof.2da~ ~override~
    ...
    LPF set_proficiency INT_VAR level = level STR_VAR kit = "%kit%" proficiency = "%proficiency%" END
    ...
PRETTY_PRINT_2DA
BUT_ONLY
```

`get_proficiency STR_VAR kit proficiency RET level`

Return the level of the proficiency for the kit as read in `weapprof.2da`. Return `-1` if either the kit or the proficiency not listed in the table file.

note(s):
* this function will only get the BG2 proficiency in case of overlapping proficiency names, e.g. `axe` and `spear`.

`set_proficiency INT_VAR level STR_VAR kit proficiency`

Set the level of the proficiency for the kit as read in `weapprof.2da`. Function PATCH_FAIL's if either the kit or the proficiency is not listed in the table file.

note(s):
* this function will only set the BG2 proficiency in case of overlapping proficiency names, e.g. `axe` and `spear`.

## D. Clab files.

Functions for manipulating kit clab files. Generally, these are just table functions specialized to clab files.

All functions in this section are patch functions. The caller is responsible for opening the file, pretty-printing, etc. A typical workflow is something like:

```weidu
LAF get_kit_clab STR_VAR kit = "%kit%" RET clab END
COPY_EXISTING ~%clab%.2da~ ~override~
    ...
    LPF append_blank_ability END
    ...
PRETTY_PRINT_2DA
BUT_ONLY
```

### D. 1. Getters.

`get_ability INT_VAR row level RET ability`

Return the ability at `row` and `level`. The returned `ability` has the form ability prefix (`AP` or `GA`), underscore and a spell resource. Function PATCH_FAIL's if either row or level are out of bounds.

### D. 2. Setters.

`set_ability INT_VAR row level STR_VAR ability prefix`

Set the ability at `row` and `level`. Function PATCH_FAIL's if `prefix` is neither `AP` nor `GA`. Function PATCH_FAIL's if either row or level are out of bounds. Resource `ability` must exist in game, otherwise function PATCH_FAIL's.

`rename_ability STR_VAR old new old_prefix new_prefix = "*"`

Renames all instances of `old` ability to `new`. Resource `new` *must* exist in game, otherwise function PATCH_FAIL's.

`delete_ability STR_VAR ability prefix`

Deletes all instances of the ability.

`append_blank_ability`

Appends a new blank ability. Named `ABILITY%row%` where row is the last row and all entries are valued `****`.

## E. HLA's.

Functions to add and remove HLA's.

## E. 1. Elementary functions.

The functions in this section manipulate the table `luabbr.2da`.

note(s):
* all functions have action and patch versions, coded via `DEFINE_DIMORPHIC_FUNCTION`.

`get_hla_table STR_VAR kit RET table`

Returns the HLA table for the `kit`. If `kit` not listed in the relevant table file (`luabbr.2da`), then it returns `*`.

note(s):
* Technically, this function only returns the first instance of the kit's HLA table; but if there are two instances, then the table is malformed.

`set_hla_table STR_VAR kit table`

Sets the HLA table for the kit. If the kit is not listed in the relevant table file (`luabbr.2da`), then function FAIL's.

note(s):
* a use case for this function is to set up a kit HLA table file different than the parent's class.

## E. 2. Normalization.

note(s):
* all functions in this section are action functions.

`normalize_hla_table STR_VAR kit`

Some hla tables miss the alignment column. This function normalizes them. The function FAIL's if the `kit` does not exist.

## E. 3. HLA table manipulation.

note(s):
* some hla tables are malformed in that they do not have the alignment column, so it is best to normalize them first using `normalize_hla_table`. 

The functions in this section manipulate HLA table files. All functions are patch functions, so the workflow is similar to that for clab files.

```
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

Adds an `hla` to the HLA table file. If `kit` not listed in the relevant table file (`luabbr.2da`) or `hla` is already present, the function FAIL's. If the hla resource `hla` does not exist, the function FAIL's.

`rename_hla STR_VAR old new old_prefix new_prefix = "*"`

Rename `old` hla to `new`. Resource `new` *must* exist in game, otherwise function PATCH_FAIL's.

```
set_hla_attributes INT_VAR
    min_level = 0 - 1
    max_level = 0 - 1
    num_allowed = 0 - 1
STR_VAR
    hla
    prefix
    icon = "*"
    strref = "*"
    prerequisite = "*"
    excluded = "*"
    alignment = "*"
```

Sets the various fields in the hla row. Note that both `prerequisite` and `excluded` have the form: prefix, underscore, resource. Both of these must already be present in the table or else the function PATCH_FAIL's.

`delete_hla STR_VAR hla prefix`

Deletes an `hla` from the hla table file. If the `hla` to delete is not in the table, the function WARN's. If `hla` is a pre-requisite of some other hla, the function PATCH_FAIL's.

note(s):
* technically, this function only removes the first instance of the `hla`; but if there are two rows with the same hla, the table is malformed.
* the function does *not* check if the deleted hla is excluded by some other hla, because in most cases the references are circular (e.g. `a` excludes `b` and `b` excludes `a`).

## F. Miscellaneous utilities.

note(s):
* all functions in this section have action and patch versions, coded via `DEFINE_DIMORPHIC_FUNCTION`.

`get_ability_resource STR_VAR ability RET resource`

Returns the resource part of an ability name, which has the form prefix (`AP` or `GA`), underscore and a spell resource.
