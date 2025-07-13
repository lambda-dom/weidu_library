# Projectiles.

A library to handle projectile .pro files.

file(s):

* [Source code](../../projectiles.tpa).

# A. Basic functions.

`get_projectile_size RET size`

The size of a (area effect) projectile in bytes.

# B. Constants.

## B. 1. Tables.

`projectile_offsets`

[Table](../../resources/2da/projectiles/offsets.2da) of projectile field offsets.

note(s):
* currently, not all fields are in the table.

# C. Readers and writers.

`get_projectile_field STR_VAR field RET value`

`set_projectile_field STR_VAR field value`

# D. Projectile functions.

note(s):
* all functions in this section have action and patch variants.

`get_projectile_id STR_VAR projectile RET id`

Return the projectile `id` associated to `projectile` in `projectl.ids`. Function returns `-1` if `projectile` not in `projectl.ids`.

note(s):
* The value looked up in `projectl.ids` is corrected by +1 to match the corresponding missile id. This is the value that is to be inserted in spell and item headers, effects, etc.

`get_projectile_res INT_VAR id RET resource`

Return the `resource` associated to the projectile numeric `id`.

note(s):
* the `id` is the value read directly from an .spl or an .itm, and is corrected by -1 to return the correct projectile resource.

`get_missile_id STR_VAR missile RET id`

Return the missile `id` associated to label `missile` in `missile.ids`. Function returns `-1` if `missile` not in `missile.ids`.

`get_missile_res STR_VAR missile RET resource`

Return the projectile `resource` associated to the `missile` label. Return `*` if `missile` not in `missile.ids`.

# E. Projectile addition.

note(s):
* all functions in this section are action functions.

`add_projectile STR_VAR projectile label = "*" dir = "*" RET id`

A slightly more convenient API for the WeiDU macro `ADD_PROJECTILE`. Copies `projectile`, a projectile resource name, adds it to the relevant projectile table and returns its assigned numeric id. If `label` is provided, the corresponding entry in `missile.ids` is set. `dir` is an optional dir where the `projectile` is located, defaulting to the standardized resources directory of the component.

# F. Patchers for `missile.ids`.

note(s):
* all functions in this section are patch functions for `missile.ids`.

`replace_missile_label STR_VAR old new`

Replaces `old` label with `new` label in `missile.ids`. The function PATCH_FAIL's if `old` is not in `missile.ids` or if `new` is.

# G. Patchers for `clearair.2da`.

note(s):
* all functions in this section are patch functions for the `clearair.2da` table.

`append_clearair STR_VAR projectile missile`

Appends `projectile` to the `clearair.2da` table. The function PATCH_FAIL's if `missile` or `projectile` are already in the table or `projectile` does not exist in-game.
