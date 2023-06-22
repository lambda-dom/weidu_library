# Miscellaneous library.

Some useful functions that are yet to find a proper home.

## A. Tables.

note(s):
* all functions in this sectionb have action and patch versions, coded via `DEFINE_DIMORPHIC_FUNCTION`.

This group of functions provides a better API for manipulating certain specific tables.

`append_clearair STR_VAR projectile label`

Appends a line to the `clearair.2da` table. The function FAIL's if `label` or `projectile` are already in the table or `projectile` does not exist in-game.