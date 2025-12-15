# References.

Resource installation is done via tables, but these have a format that implies certain restrinctions in the values (for example, no spaces). This library introduces a tiny dsl to allow more complex expressions.

A *table reference*, as used in several .2da tables used by installer libraries, has the following regexp format:

```regexp
^#([a-zA-Z0-9][a-zA-Z0-9_-]*):(.*)$
```

The first group, an alpha-numeric identifier, uniquely identifies the function that is to be called (currently all examples are three-letter identifiers -- see below), while the second group, is the argument to pass to it. The string it returns can be anything, but is usually a string or number that has passed some validation checks. In short, and denoting the first group by `function` and the second by `value`, this is inline notation for the call

```weidu
LAF "%function%" STR_VAR value = "%value% RET resource
```

Each `function` is free to parse `value` as necessary.

file(s):

* [Source code](../../references.tpa).

# A. Main function.

note(s):
* All functions in this section have patch and action variants.

`encode_table_reference STR_VAR value RET return`

This is the main entry point of the library, and parses a `value` into a function call. In details: parses the string `value` against the regexp `^#([a-zA-Z0-9][a-zA-Z0-9_-]*):(.*)$` and grabs the extracted function's name and the argument value. If `value` does not match the regexp, the function FAIL's. If it matches, lookup the name in a table of `name => function` pairs and return whatever the function call returns:

```weidu
LPF "%function%" STR_VAR value = "%value%" RET return
```

Note the signature of the called function: one argument named `value` and the return value named `return` -- the signature of an *encoder*. The available formats are detailed in the formats section.

# A. 1. Available formats.

`reference_encoders`

Array of `format => encoder` pairs.

# B. Formats.

The following functions are the available encoders. There is usually no need to call them directly, rather call them indirectly with `encode_table_reference`.

## B. 1. String formats.

`encode_resource_literal STR_VAR value RET return`

Treats `value` as a literal and returns it unchanged, except for upper-casing. Format is:

```
#lit:<resource reference>
```

note(s):
* it also checks the length, that is, if length of the resource reference is strictly larger than 8 the function FAIL's.

`encode_empty_string STR_VAR value RET return`

Returns the empty string. Format is:

```
#nul:
```

Note that value is the empty string; if anything follows the colon, the function FAIL's.

## B. 2. Numeric formats.

`encode_num_literal STR_VAR value RET return`

Treats `value` as an integer numeric literal and returns it. Format is:

```
#num:<numeric literal>
```

Both (signed) decimal and hex literals are accepted.

note(s):
* this is useful mainly if the values in a given column can be either numbers or some other kind of object, and this provides a way to disambiguate. If all values must be integers (as checked by the table processing code) there is little point in using this format. One use case is the [Blocks library](./blocks.md) where the column values can have various interpretations depending on the value of another column (e.g. this is a (very) primitive form of dependent typing).

## B. 3. Spell-related formats.

`encode_spell_res STR_VAR value RET return`

Treats `value` as a symbolic spell reference in `spell.ids` and returns the corresponding resource reference. Function FAIL's if `value` not present in `spell.ids`. Format is:

```
#spl:<spell symbolic reference>
```

`encode_spell_suffix STR_VAR value RET return`

Returns the symbolic spell reference suffixed with the character. For example, e.g. `a:CLERIC_BLESS` returns `sppr101a`. Function FAIL's if the spell symbol (last component) not present in `spell.ids`. Format is:

```
#suf:<one alphanumeric character>:<spell symbolic reference>
```

`encode_spell_affix STR_VAR value RET return`

Returns the symbolic spell reference suffixed with a character and the first two characters relaced by the affix. For example, e.g. `dv:a:CLERIC_BLESS` returns `dvpr101a`. Function FAIL's if the spell symbol (last component) not present in `spell.ids` or the returning value is longer than 8 characters. Format is:

```
#afx:<two alphanumeric characters>:<one alphanumeric character>:<spell symbolic reference>
```

`encode_extended_spell_resource STR_VAR value RET return`

Treats `value` as a symbolic spell reference in the extended namespace table and returns the corresponding resource reference. Function FAIL's if `value` not present in the table. Format is:

```
#spe:<spell symbolic reference>
```

note(s):
* Safe use of this function requires no changes to the master .2da file before the last `CLEAR_ARRAYS`. The safest way to ensure it is to put all changes in a (sub)component and all uses of the function is a different (sub)component.

## B. 4. Projectile-related formats.

`encode_missile_res STR_VAR value RET return`

Treats `value` as a symbolic projectile reference in `missile.ids` and returns the corresponding resource reference. Function FAIL's if `value` not present in `spell.ids`. Format is:

```
#lbl:<missile reference>
```

note(s):
* Function from [Encoders](./encoders.md).

## B. 5. Opcode-related formats.

`encode_opcode_type STR_VAR value RET return`

Returns the numeric id of an opcode type. Function FAIL's if `value` not present in [Opcodes table](../../resources/2da/opcodes/types.2da). Format is:

```
#opc:<opcode type>
```

## B. 6. Sectype-related formats.

`encode_spell_sectype STR_VAR value RET return`

Returns the numeric id of a sectype. Function FAIL's if `value` is not a valid sectype. Associated format is:

```
#sct:<sectype>
```

## B. 7. Resource extension.

`encode_resource_extension STR_VAR value RET return`

Returns a resource reference, checking its in-game existence. Associated format is:

```
#ext:<ext>:<resource reference>
```

`<ext>` is a 3-letter resource extension (e.g. `bam`) and `<resource reference>` is a resource reference parsed with a call to `encode_table_reference`.

note(s):
* this format is used in the (rare) case where a column contains resource references but their type can vary and one needs existence validation.

# C. Other resource encoders.

The next set of encoders have no format associated and are mainly used as value sanitizers.

`encode_bam_ref STR_VAR value RET return`

`encode_projectile_ref STR_VAR value RET return`

`encode_script_ref STR_VAR value RET return`

`encode_dialog_ref STR_VAR value RET return`

These encoders parse a resource reference for a resource of the appropriate type, do an extra in-game existence check and return the value.
