# Patchers.

Library of patchers of all kinds.

file(s):

* [Source code](../../patchers.tpa)

# A. Spell patchers.

`add_display_string INT_VAR tra_ref insert_point = 0 - 1`

Add a Display String [139] opcode at `insert_point` (default is appending) to all the headers of a spell. The text to be displayed is the tra reference `tra_ref`. Timing is instant and target is creature (other).

# B. Creature patcher.

`creature_add_item STR_VAR reference slot flags array`
