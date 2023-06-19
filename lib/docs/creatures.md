# The Creatures library.

A utilities library to handle creature .cre files.

## A. Constants.

`creature_size`

(Minimum) size (in bytes) of a creature resource.

`creature_offsets`

Array of cre offsets.

note(s):
* some fields are not yet listed.

## B. Basic functions.

note(s):
* all functions in this section are patch functions.

`get_cre_field STR_VAR field RET value`

Generic read function. Return the `value` of creature `field`. If the field is not an creature field, function PATCH_FAIL's.

note(s):
* casing of `field` is irrelevant.

`set_cre_field STR_VAR field value`

Generic write function. Write `value`, passed as a string, to `field` of creature. If the field is not a creature field, function PATCH_FAIL's.

note(s):
* casing of `field` is irrelevant.
* pay attention to the types of the fields, so as not to pass the wrong argument and get a clobbered file. These can be checked in the [creature_offsets.2da](../resources/2da/creature_offsets.2da) table.

