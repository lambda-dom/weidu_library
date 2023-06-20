# The subspells effects library.

A higher-level library to install subspells via standardized cloning.

## A. Functions.

note(s):
* all functions in this section have action and patch versions, coded via `DEFINE_DIMORPHIC_FUNCTION`.

`clone_subspell_from_table INT_VAR school = 0 sectype = 0 STR_VAR spell dest arguments`

Clones a spell from a hardcoded table, copying it into the game folder as dest. The function will FAIL if a similarly named resource already exists. The `arguments` argument is an associative array to forward to the patchers. The meaning of each argument depends on the specific spell. The function automatically fills in the description, mostly for documentation purposes, using `arguments` and the in-library description.

The `school` and `sectype` arguments are integer arguments to set the school and sectype of the subspell. For correct interaction with various opcodes, in general, subspells should have the same school and sectype as the parent spell. The general workflow is something:

```
DEFINE_PATCH_FUNCTION patch_parent_spell BEGIN
    ...
    LPF get_spell_field STR_VAR field = "sectype" RET sectype = value END
    ...
    LPF clone_subspell_from_table INT_VAR sectype = sectype ...
END
```

note(s):
* all the information for any given spell is in the [table subspells.2da](../resources/2da/subspells.2da).
* standardized subspell patches are in `subspell_patches.tpa`; these are called automatically by the `clone_subspell_from_table` function when copying the spell. Each patch has signature `STR_VAR arguments` with `arguments` an associative array containing the needed arguments. One convention that is used throughout the patching code is to name the resource, for opcode resource fields, as `self#res`.

note(s): implementation notes:
* the cloned subspell is uniquely determined by the `arguments`so the results could be cached. The caching scheme would be a table with keys the `dest` and values the argument values. Currently, this is not implemented.