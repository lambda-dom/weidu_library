# Changelog for `weidu_library`

## version v1.0beta2 -- unreleased.

* Drop mutators from base spells and items libraries.
* Re-introduce mutators in the form of `insert_*_header` and `insert_*_opcode` functions.
* Drop array functions from spells and items libraries.
* Change `load_2da_table` to return an array indexed by column *names*.
* Fix `is_key_in_array`.
* Remove uses of `is_key_in_array`.

## version v1.0beta1.

* Initial release.
* Drop sounds from spell installer.

## version v1.0alpha6.

* Changes to entangle and fear subspells.
* Allow directly setting school and sectype of subspells.
* Add sleep subspell; tighten immunities of unconsciousness.
* Add slow subspell.
* Add `copy_data_resource` function.
* Miscellaneous library.
* Function `copy_resources_from_table`.
* Function `copy_projectiles_from_table`.
* Removed resource installation from spl and itm installers.
* `load_file` behaves as `load_component` on entry and `CLEAR`'s.
* Opcode arrays library.
* Dropped Patching library.

## version v1.0alpha5.

* Add `dir` argument to `patch_opcode_block`.
* General pass to enforce case-insensivity almost everywhere.

## version v1.0alpha4.

* Small readme corrections.
* Add `load_2da_table`.
* Delete spurious `copy_items_template.2da`.
* Added `opcode_types` array and `get_opcode_type` function.
* Add `patching` library.
* Change `get_array_element`.
* Some code and resources moved around. 

## version v1.0alpha3.

* Move final patching in `copy_items_from_table` to its own `COPY_EXISTING` block to ensure that calls to `set_ability_tooltip` and similar functions do not barf on new items as the documentation states.
* Same change for `copy_cres_from_table`.
* Add `biography` to `creature_offsets.2da`.
* Add ids entries to `copy_cres_from_table` and `patch_cre`.
* Fix defaulting on exclusion flags.

## version v1.0alpha2.

* Bug fixes in hla functions.
* New `insert_item_header` to insert headers in items.
* Add fields to `copy_cres_from_table` and `patch_cre`.

## version v1.0alpha1.

Initial release.
