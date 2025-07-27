# The Kits library.

A library to patch kits.

file(s):

* [Source code](../../kits.tpa).

# A. Basic functions.

note(s):
* all functions in this section have both action and patch versions.

`get_kit_clab STR_VAR kit RET clab`

Return the kit's clab file. Returns `*` if kit is not present in `kitlist.2da`.

note(s):
* this function opens `kitlist.2da` on each call, to search for the kit.
* technically, this returns the first `kit` match, but if there are two entries for the same kit in `kitlist.2da`, then the table is malformed.

# B. Descriptions.

note(s):
* all functions in this section have both action and patch versions.

`set_class_description INT_VAR descr STR_VAR class`

Set the description of a class in the .2da files `clastext.2da` and `enginest.2da`. `descr` is a tra reference. Function FAIL's if kit not found in the relevant tables.

note(s):
* this function has the side-effect of (potentially) adding the text of the tra reference to the tlk file.

`set_kit_description INT_VAR descr STR_VAR kit`

Set the new description of a kit in the .2da files `kitlist.2da`, `clastext.2da` and `enginest.2da`. `descr` is a tra reference. Function FAIL's if kit not found in the relevant tables.

note(s):
* this function has the side-effect of (potentially) adding the text of the tra reference to the tlk file.
* in the EE's you usually have to call `set_class_description` for a kit as well. To make matters worse, this does *not* cover all class descriptions used by the engine (some of these are hard-coded and picked up in the ui).

# C. Proficiencies.

All functions in this section are patch functions for the table `weapprof.2da`. The caller is responsible for opening the file, pretty-printing, etc. A typical workflow would be something like:

```weidu
COPY_EXISTING "weapprof.2da" "override"
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

`patch_proficiencies STR_VAR kit array`

Patch a kit's proficiencies using a an array `proficiency => amount`.

# D. Abilities.

All functions in this section are patch functions for clab table files like `clab*.2da`. The caller is responsible for opening the file, pretty-printing, etc.

`make_clab_replacements STR_VAR array`

Patch resource references in a clab file using an `array` of references, loaded via `get_table_references` from the [installers library](./installers.md).

note(s):
* this function is slow; it has to crawl through the entire clab, check if the reference is in the `array` and if it is, set it.
