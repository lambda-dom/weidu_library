# Patchers.

Library of patchers of all kinds.

file(s):

* [Source code](../../../internal/patchers.tpa)

# A. Spell patchers.

`add_display_string INT_VAR tra_ref insert_point = 0 - 1`

Add a Display String [139] opcode at `insert_point` (default is appendin) to all the headers of a spell. The text to be displayed is the tra reference `tra_ref`. Timing is instant and target is creature, or other.
