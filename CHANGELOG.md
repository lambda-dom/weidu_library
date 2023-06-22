# Changelog for `weidu_library`

## version v1.0beta6 -- unreleased.

* Changes to entangle and fear subspells.
* Verbose flags in `patch_opcode_block`.
* Allow directly setting school and sectype of subspells.
* Suite of opcode array functions.
* Add sleep subspell; tighten immunities of unconsciousness.
* Add slow subspell.
* Add `copy_data_resource` function.
* Miscellaneous library.
* Function `copy_resources_from_table`.

Changed to beta releases, as some libraries are still in a state of flux, namely [Patching](./lib/docs/patching.md), and all the supporting code, currently located in the [Opcodes](./lib/docs/opcodes.md) library.

## version v1.0beta5.

* Add `dir` argument to `patch_opcode_block`.
* General pass to enforce case-insensivity almost everywhere.

## version v1.0beta4.

* Small readme corrections.
* Add `load_2da_table`.
* Delete spurious `copy_items_template.2da`.
* Added `opcode_types` array and `get_opcode_type` function.
* Add `patching` library.
* Change `get_array_element`.
* Some code and resources moved around. 

## version v1.0beta3.

* Move final patching in `copy_items_from_table` to its own `COPY_EXISTING` block to ensure that calls to `set_ability_tooltip` and similar functions do not barf on new items as the documentation states.
* Same change for `copy_cres_from_table`.
* Add `biography` to `creature_offsets.2da`.
* Add ids entries to `copy_cres_from_table` and `patch_cre`.
* Fix defaulting on exclusion flags.

## version v1.0beta2.

* Bug fixes in hla functions.
* New `insert_item_header` to insert headers in items.
* Add fields to `copy_cres_from_table` and `patch_cre`.

## version v1.0beta1.

Initial release.
