# The Effects library

A library to handle extended effect .eff files.

## A. Constants.

`effect_size`

Size (in bytes) of an extended effect.

`effect_offsets`

Array of extended effect offsets. The field names are the same as in WeiDU macros like `ADD_EFFECT`.

## B. Basic functions.

note(s):
* all functions in this section are patch functions.

`get_effect_field STR_VAR field RET value`

Generic read function. Return the `value` of effect `field`. If the field is not an effect field, function PATCH_FAIL's.

note(s):
* casing of `field` is irrelevant.

`set_effect_field STR_VAR field value`

Generic write function. Write `value`, passed as a string, to `field` of effect. If the field is not an effect field, function PATCH_FAIL's.

note(s):
* casing of `field` is irrelevant.
* pay attention to the types of the fields, so as not to pass the wrong argument and get a clobbered file. These can be checked in the [effect_offsets.2da](../resources/2da/effect_offsets.2da) table.

## C. Builders.

note(s):
* all functions in this section have action and patch versions, coded via `DEFINE_DIMORPHIC_FUNCTION`.

`create_effect_with_array INT_VAR opcode STR_VAR resource arguments`

A slightly more covenient interface to `CREATE EFF` to create effects on the fly. `resource` is the resource name, and the function FAIL's if it already exists in game. `arguments` is an array, passed by name, of pairs `field => value` with which to patch the effect via `set_effect_field`.
