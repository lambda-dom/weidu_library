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

## B. Opcode functions.

note(s):
* all functions in this section are patch functions.

`get_opcode_field INT_VAR offset STR_VAR field RET value`

Generic read function. Return the value of `field` of opcode at `offset`. If field is not an opcode field, function PATCH_FAIL's.

`set_opcode_field INT_VAR offset = 0 STR_VAR field value`

Generic write function. Write `value`, passed as a string, to `field` of opcode at `offset`. If the field is not an opcode field, function PATCH_FAIL's.

note(s):
* pay attention to the types of the fields, so as not to pass the wrong argument and get a clobbered file. These can be checked in the [opcode_offsets.2da](../resources/2da/opcode_offsets.2da) table.

`match_opcode_against_array INT_VAR offset = 0 STR_VAR array RET bool`

Matches opcode at `offset` field by field against the `array` fields. PATCH_FAIL's if any of the array fields is not an opcode field. Array `array` is passed by name.

note(s):
* arguments stuffed in an array to simplify the function's signature.

## C. Opcode field utilities.

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
* the symbolic names can be found in the [opcode_targets.2da table](../resources/2da/opcode_targets.2da).

`get_opcode_timing STR_VAR timing RET value`

Return the integer `value` corresponding to the symbolic name of opcode's `timing`. The function returns -1 if `timing` is not valid.

note(s):
* the symbolic names can be found in the [opcode_timings.2da table](../resources/2da/opcode_timings.2da).

`get_opcode_dispel_resistance STR_VAR dispel_resistance RET value`

Return the integer `value` corresponding to the symbolic name of opcode's `dispel_resistance`. The function returns -1 if `dispel_resistance` is not valid.

note(s):
* the symbolic names can be found in the [opcode_dispel_resistance.2da table](../resources/2da/dispel_resistance.2da).