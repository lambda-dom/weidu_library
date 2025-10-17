# The Creatures library.

A library to handle creature .cre files.

file(s):

* [Source code](../../creatures.tpa).

# A. Constants.

## A. 1. Tables.

`cre_offsets`

The [Table](../../resources/2da/creatures/offsets.2da) of cre offsets.

## A. 2. Arrays.

`item_slots`

The [Array](../../resources/2da/creatures/item_slots.2da) of cre item slots.

# B. Basic functions.

`get_cre_size RET size`

Return the `size` of a creature file in bytes.

# C. Field functions.

Basic reading functions that return the values of read-only creature fields that should not, and cannot (e. g. via the generic `set_field`), be set.

`get_cre_known_spell_count RET count`

`get_cre_known_spell_offset RET offset`

`get_cre_memorized_spell_count RET count`

`get_cre_memorized_spell_offset RET offset`

`get_cre_item_count RET count`

`get_cre_effect_count RET count`

# D. Readers and writers.

Specializations of the generic reader and writer for creature files.

`get_cre_field STR_VAR field RET value`

`set_cre_field STR_VAR field value`

# E. Encoders.

`encode_creature_slot_id STR_VAR value RET return`

`encode_creature_animation_id STR_VAR value RET return`
