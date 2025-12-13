# The Spell symbols library.

Library for doing surgery in `spell.ids`.

file(s):

* [Source code](../../spell_symbols.tpa).

# A. `spell.ids` patching.

## A. 1. Action functions.

note(s):
* All functions in this section are action functions that patch `spell.ids`, essentially wrappers around the `ADD_SPELL` macro.

`add_spell_symbol INT_VAR level STR_VAR symbol type patch = "*"`

A wrapper around the WeiDU `ADD_SPELL` action macro. The function FAIL's if `symbol` already exists in `spell.ids`, `type` is not a valid spell type to add (see [Add spell types](../../resources/2da/spells/add_types.2da)) or `level` is not an integer in the [0-9] range. `patch` is the name of an optional patch function; the function must be in scope and will be called with no arguments.

The spell resource used is a generic, black spell. It is expected that it is overriden later in the install.

`change_spell_symbol INT_VAR level STR_VAR symbol type`

Changes the spell `symbol` to `type` and `level`. This is implemented as a call to `ADD_SPELL` where `symbol` must already exist in `spell.ids`. It adds a new slot to `spell.ids` unless `type` and `level` are the same, in which case the call is a no-op. The original spell resource is untouched.

## A. 2. Patchers.

note(s):
* Unless explicitly said otherwise, all functions in this section are patching functions for `spell.ids`.

`alias_spell_symbol STR_VAR symbol aliased`

This function changes `symbol` to reference the same spell resource of `aliased`. The function fails if either `symbol` or `aliased` do not exist in `spell.ids`.

note(s):
* This function explicitly breaks the injectivity rule, so it is wise to subsequently change `aliased` to something else.

`replace_spell_symbol STR_VAR new old`

Replaces spell symbol `old` with `new`. The function FAIL's if either `old` is not present in `spell.ids` or `new` is. The underlying spell resource is left untouched.

note(s):
* This function makes the `old` spell symbol unavailable so any code that relies on its existence will fail.
* This is a slow operation.

`deprecate_spell_symbol STR_VAR symbol`

Deprecates spell `symbol` by replacing it with `symbol_DEPRECATED`. The spell resource is left untouched.

note(s):
* This function makes the spell `symbol` unavailable so any code that relies on its existence will fail. It also has the potential to break the injectivity rule as the underlying spell resource is now free.

`assign_spell_symbol_hole INT_VAR level id STR_VAR symbol type`

Assign a hole in `spell.ids` (unassigned slot) to the spell symbol `symbol`. The function fails if `level` or `id` are out of bounds, `type` is not a valid spell type, the slot is already assigned or `symbol` already exists in `spell.ids`.
