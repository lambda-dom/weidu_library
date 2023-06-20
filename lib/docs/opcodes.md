# The Opcodes library

A utilities library to handle the processing of opcodes.

## A. Constants.

`opcode_size`

The size of an opcode in bytes.

`opcode_offsets`

Array of (relative) opcode offsets. The field names are the same as in WeiDU macros like ADD_EFFECT.

`opcode_targets`

Array with keys the target symbolic names and values the corresponding values.

`opcode_timings`

Array with keys the timing symbolic names and values the corresponding values.

`opcode_dispel_resistance`

Array with keys the dispellable/mr-affected symbolic names and values the corresponding values.

`opcode_types`

Array of pairs `type => number`. The map is bidirectional, but no advantage is taken of this (yet).

note(s):
* only opcodes for BG(2)EE are in the table.

## B. Opcode functions.

note(s):
* all functions in this section are patch functions.

`get_opcode_field INT_VAR offset STR_VAR field RET value`

Generic read function. Return the value of `field` of opcode at `offset`. If field is not an opcode field, function PATCH_FAIL's.

note(s):
* casing of `field` is irrelevant.

`set_opcode_field INT_VAR offset = 0 STR_VAR field value`

Generic write function. Write `value`, passed as a string, to `field` of opcode at `offset`. If the field is not an opcode field, function PATCH_FAIL's.

note(s):
* casing of `field` is irrelevant.
* pay attention to the types of the fields, so as not to pass the wrong argument and get a clobbered file. These can be checked in the [opcode_offsets.2da](../resources/2da/opcode_offsets.2da) table.

## C. Array opcode functions.

`get_opcode_array INT_VAR offset RET_ARRAY array`

Return the associative array of pairs `field => value` of opcode at `offset`.

`match_opcode_against_array INT_VAR offset = 0 STR_VAR array RET bool`

Matches opcode at `offset` field by field against the `array` fields. PATCH_FAIL's if any of the array fields is not an opcode field. Array `array` is passed by name.

note(s):
* casing of *both* fields and values in the array is irrelevant.

```
create_opcode_array INT_VAR
    opcode = 0
    target = 0
    power = 0
    parameter1 = 0
    parameter2 = 0
    timing = 0
    duration = 0
    resist_dispel = 0
    probability1 = 100
    probability2 = 0
    dicenumber = 0
    dicesize = 0
    savingthrow = 0
    savebonus = 0
    special = 0
STR_VAR
    opcode_array = ""
    resource = ""
RET_ARRAY
    array
```

Construct an opcode array by merging an array of defaults given by the various opcode fields and `opcode_array`, an array passed by name. Only valid field names in `opcode_array` are considered. No error checking is done so the values can be arbitrary.

note(s):
* this function has both patch and action variants, coded via `DEFINE_DIMORPHIC_FUNCTION`.

`write_opcode_array INT_VAR offset STR_VAR array`

Write the various opcode fields in `array` to opcode at `offset`. Only valid field names in `opcode_array` are considered. The function does extensive error checking to avoid inserting garbage data. The fields `opcode`, `target`, `timing` and `resist_dispel` use symbolic names and these are checked for validity.

note(s):
* casing of array fields is irrelevant.

## D. Opcode field utilities.

This group of functions is designed to make it safer to mutate opcodes and not insert rubbish data. Unfortunately, because of fundamental limitations of the WeiDU language, using these ends up being a veritable PITA. To see this, consider the simplest example of inserting a valid target value into an opcode:

```weidu
LPF get_opcode_target STR_VAR target = "%target%" RET value END
LPF set_opcode_field STR_VAR field = "target" value = "%value%" END
```

Setting aside, the error handling, one immediately sees the problem: a function call in WeiDU is syntactically *extremely verbose* and unwieldy, requiring intermediate variables to pass around values. Compare this with, say, the python equivalent snippet:

```python
set_opcode_field(field = "target", value = get_opcode_target(target))
```

note(s):
* all functions in this section have patch and action versions coded via `DEFINE_DIMORPHIC_FUNCTION`.

`get_opcode_target STR_VAR target RET value`

Return the integer `value` corresponding to the symbolic name of opcode's `target`. The function returns -1 if `target` is not valid.

note(s):
* casing of `target` is irrelevant.
* the symbolic names can be found in the [opcode_targets.2da table](../resources/2da/opcode_targets.2da).

`get_opcode_timing STR_VAR timing RET value`

Return the integer `value` corresponding to the symbolic name of opcode's `timing`. The function returns -1 if `timing` is not valid.

note(s):
* casing of `timing` is irrelevant.
* the symbolic names can be found in the [opcode_timings.2da table](../resources/2da/opcode_timings.2da).

`get_opcode_resist_dispel STR_VAR resist_dispel RET value`

Return the integer `value` corresponding to the symbolic name of opcode's `resist_dispel`. The function returns -1 if `resist_dispel` is not valid.

note(s):
* casing of `resist_dispel` is irrelevant.
* the symbolic names can be found in the [opcode_resist_dispels.2da table](../resources/2da/opcode_resist_dispels.2da).

`get_opcode_type STR_VAR type RET value`

Return the integer `value` corresponding to the symbolic name of the opcode's `type`. The function returns -1 if `type` is not valid.

note(s):
* casing of `type` is irrelevant.
* the symbolic names of the opcode types can be found in the [opcode_types.2da table](../resources/2da/opcode_types.2da).