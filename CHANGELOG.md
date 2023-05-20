# Changelog for `weidu_library`

## version v1.0rc3.

* Move final patching in `copy_items_from_table` to its own `COPY_EXISTING` block to ensure that calls to `set_ability_tooltip` and similar functions do not barf on new items as the documentation states.
* Same change for `copy_cres_from_table`.
* Add `biography` to `creature_offsets.2da`.

## version v1.0rc2.

* Bug fixes in hla functions.
* New `insert_item_header` to insert headers in items.
* Add fields to `copy_cres_from_table` and `patch_cre`.

## version v1.0rc1.

Initial release.
