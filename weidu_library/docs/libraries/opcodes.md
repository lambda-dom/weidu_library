# The Opcodes library.

A library to handle the processing of opcodes.

file(s):

* [Source code](../../opcodes.tpa).

# A. Basic functions.

`get_opcode_size RET size`

Return the `size` of an opcode in bytes.

# B. Constants.

All tables and arrays below are loaded on `INCLUDE`-ing.

## B. 1. Tables.

`opcode_offsets`

The [table](../../resources/2da/opcodes/offsets.2da) of relative opcode offsets. The field names are the same as in WeiDU macros like `ADD_ITEM_EQEFFECT`.

## B. 2. Arrays.

`opcode_types`

The [array](../../resources/2da/opcodes/types.2da) of pairs opcode `type => id`.

`opcode_targets`

The [array](../../resources/2da/opcodes/targets.2da) of pairs opcode `target => id`.

`opcode_timings`

The [array](../../resources/2da/opcodes/timings.2da) of pairs opcode `timing mode => id`.

`opcode_resist_dispels`

The [array](../../resources/2da/opcodes/resist_dispels.2da) of pairs opcode `dispel/resist mode => id`.

`save_flags`

The [array](../../resources/2da/opcodes/save_flags.2da) of pairs `save flag => bit index`.

`damage_modes`

The [array](../../resources/2da/opcodes/damage_modes.2da) of pairs `damage mode => int`.

`damage_types`

The [array](../../resources/2da/opcodes/damage_types.2da) of pairs `damage type => int`.

`ids_ids`

The `array` of [pairs](../../resources/2da/opcodes/ids.2da) `ids => id` of ids files and their associated id's, as used in opcodes like Use Eff [177].

# C. Getters.

The next set of functions convert a value in a human-readable format like an opcode type, to their corresponding numeric id, usually to be written out in binary format.

`get_opcode_type_id STR_VAR value RET id`

`get_opcode_target_id STR_VAR value RET id`

`get_opcode_timing_id STR_VAR value RET id`

`get_opcode_resist_dispel_id STR_VAR value RET id`

`get_save_flag_index STR_VAR value RET index`

`get_ids_file_id STR_VAR file RET id`

# D. Readers and writers.

Specializations of the generic reader and writer for opcodes.

`get_opcode_field INT_VAR offset STR_VAR field RET value`

`set_opcode_field INT_VAR offset STR_VAR field value`
